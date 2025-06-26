# Kerberos Linux Client

### Kerberos Client Linux Setup

[Installation Guide](https://web.mit.edu/kerberos/krb5-devel/doc/user/tkt_mgmt.html)

* Update repositories before installation

```
    [INPUT]
    sudo apt update

    [OUTPUT]
    [...]
    Get:16 http://cdn-aws.deb.debian.org/debian bullseye-backports/main Translation-en [299 kB]
    Fetched 24.9 MB in 5s (4744 kB/s)
    Reading package lists... Done
    Building dependency tree... Done
    Reading state information... Done
    56 packages can be upgraded. Run 'apt list --upgradable' to see them.
Install packages
```

* Install packages

```
    [INPUT]
    sudo apt install krb5-user -y

    [OUTPUT]
    [GUI] - always answer "KRBSRV.LIN3"
    [...]
    Setting up krb5-config (2.6+nmu1) ...
    Setting up libkadm5clnt-mit12:amd64 (1.18.3-6+deb11u3) ...
    Setting up libkdb5-10:amd64 (1.18.3-6+deb11u3) ...
    Setting up libkadm5srv-mit12:amd64 (1.18.3-6+deb11u3) ...
    Setting up krb5-user (1.18.3-6+deb11u3) ...
    Processing triggers for man-db (2.9.4-2) ...
    Processing triggers for libc-bin (2.31-13+deb11u3) ...
```

* Config Kerberos

REAL: KRBSRV.LIN3

Note: this config file was generated during initial setup (GUI)

```
    [libdefaults]
        default_realm = KRBSRV.LIN3

    # The following krb5.conf variables are only for MIT Kerberos.
            kdc_timesync = 1
            ccache_type = 4
            forwardable = true
            proxiable = true

    # The following encryption type specification will be used by MIT Kerberos
    # if uncommented.  In general, the defaults in the MIT Kerberos code are
    # correct and overriding these specifications only serves to disable new
    # encryption types as they are added, creating interoperability problems.
    #
    # The only time when you might need to uncomment these lines and change
    # the enctypes is if you have local software that will break on ticket
    # caches containing ticket encryption types it doesn't know about (such as
    # old versions of Sun Java).

    #       default_tgs_enctypes = des3-hmac-sha1
    #       default_tkt_enctypes = des3-hmac-sha1
    #       permitted_enctypes = des3-hmac-sha1

    # The following libdefaults parameters are only for Heimdal Kerberos.
            fcc-mit-ticketflags = true

    [realms]
            KRBSRV.LIN3 = {
                    kdc = KRBSRV.LIN3
                    admin_server = KRBSRV.LIN3
            }
```

* Setup local DNS

```
    [INPUT]
    sudo vi /etc/cloud/templates/hosts.debian.tmpl

    //Add KRBSRV.LIN3 record
    10.0.2.11   KRBSRV.LIN3
```

```
    [INPUT]
    sudo reboot
```

* Validate DNS entry

```
    [INPUT]
    ping KRBSRV.LIN3

    [OUTPUT]
    PING KRBSRV.LIN3 (10.0.2.11) 56(84) bytes of data.
    64 bytes from KRBSRV.LIN3 (10.0.2.11): icmp_seq=1 ttl=64 time=0.973 ms
    64 bytes from KRBSRV.LIN3 (10.0.2.11): icmp_seq=2 ttl=64 time=0.418 ms
```

* Get ticket

```
    [INPUT]
    kinit ubuntu/admin
    Password for ubuntu/admin@KRBSRV.LIN3:***
```

* Get ticket details

```
    [INPUT]
    klist

    [OUTPUT]
    Ticket cache: FILE:/tmp/krb5cc_1000
    Default principal: ubuntu/admin@KRBSRV.LIN3

    Valid starting     Expires            Service principal
    12/08/22 17:06:26  12/09/22 03:06:26  krbtgt/KRBSRV.LIN3@KRBSRV.LIN3
            renew until 12/09/22 17:06:21
```
