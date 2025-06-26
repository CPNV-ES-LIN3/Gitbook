# Kerberos Server - Ubuntu

## Kerberos Server Setup

### Infra

* Kerberos Server : Ubuntu 22.04
* Kerberos Lin Client : Debian 11
* Kerberos Win Client : W2k22

### Kerberos Server Setup

[Installation Guide](https://ubuntu.com/server/docs/service-kerberos)

[Kadmin Guide](https://web.mit.edu/kerberos/krb5-1.12/doc/admin/admin_commands/kadmin_local.html)

* Update repositories before installation

```
    [INPUT]
    sudo apt update

    [OUTPUT]
    [...]
    Get:41 http://eu-west-1.ec2.archive.ubuntu.com/ubuntu jammy-backports/universe amd64 c-n-f Metadata [348 B]
    Get:42 http://eu-west-1.ec2.archive.ubuntu.com/ubuntu jammy-backports/multiverse amd64 c-n-f Metadata [116 B]
    Fetched 25.0 MB in 5s (5403 kB/s)
    Reading package lists... Done
    Building dependency tree... Done
    Reading state information... Done
    96 packages can be upgraded. Run 'apt list --upgradable' to see them.
```

* Install packages

```
    [INPUT]
    sudo apt install krb5-kdc krb5-admin-server -y

    [OUTPUT]
    [GUI] - always answer "KRBSRV.LIN3"
    [...]
    Processing triggers for libc-bin (2.35-0ubuntu3.1) ...
    Processing triggers for man-db (2.10.2-1) ...
    Scanning processes...
    Scanning linux images...

    Running kernel seems to be up-to-date.

    No services need to be restarted.

    No containers need to be restarted.

    No user sessions are running outdated binaries.

    No VM guests are running outdated hypervisor (qemu) binaries on this host.
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

* Set Kerberos Admin Server as a service

```
    [INPUT]
    sudo systemctl enable krb5-admin-server.service

    [OUTPUT]
    Synchronizing state of krb5-admin-server.service with SysV service script with /lib/systemd/systemd-sysv-install.
    Executing: /lib/systemd/systemd-sysv-install enable krb5-admin-server
    sudo systemctl enable krb5-kdc.service
```

* Set Keberos KDC as a service

```
    [INPUT]
    sudo systemctl enable krb5-kdc.service

    [OUTPUT]
    Synchronizing state of krb5-kdc.service with SysV service script with /lib/systemd/systemd-sysv-install.
    Executing: /lib/systemd/systemd-sysv-install enable krb5-kdc
```

* Create Kerberos Database

```
    [INPUT]
    sudo kdb5_util create -r KRBSRV.LIN3 -s
    
    [OUTPUT]
    Loading random data
    Initializing database '/var/lib/krb5kdc/principal' for realm 'KRBSRV.LIN3',
    master key name 'K/M@KRBSRV.LIN3'
    You will be prompted for the database Master Password.
    It is important that you NOT FORGET this password.
    Enter KDC database master key:****
    Re-enter KDC database master key to verify:****
```

* Create an admin for Kerberos Administration

```
    [INPUT]
    sudo kadmin.local

    [OUTPUT]
    Authenticating as principal root/admin@KRBSRV.LIN3 with password.
    
    [INPUT]
    kadmin.local:  addprinc ubuntu/admin

    [OUTPUT]
    No policy specified for ubuntu/admin@KRBSRV.LIN3; defaulting to no policy
    Enter password for principal "ubuntu/admin@KRBSRV.LIN3": ****
    Re-enter password for principal "ubuntu/admin@KRBSRV.LIN3": ****
    Principal "ubuntu/admin@KRBSRV.LIN3" created.
```

* Update ACL for this new user

```
    [INPUT]
    sudo vi /etc/krb5kdc/kadm5.acl

    //Add this line (new file)
    ubuntu/admin@KRBSRV.LIN3    *
```

```
    [INPUT]
    sudo systemctl restart krb5-admin-server.service

    [OUTPUT]
    -none-
```

* Fix the hostname and make it persistent [AWS Guide](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/set-hostname.html)

```
    [INPUT]
    sudo hostnamectl set-hostname KRBSRV.LIN3
    hostname

    [OUTPUT]
    KRBSRV.LIN3
```

```
    [INPUT]
    sudo vi /etc/cloud/cloud.cfg

    //update false value in true
    preserve_hostname: true
```

* Reboot needed (restart krb service may enough)
* Ask ticket

```
    [INPUT]
    kinit ubuntu/admin

    [OUTPUT]
    Password for ubuntu/admin@KRBSRV.LIN3: ****
```

* Get ticket details

```
    [INPUT]
    ubuntu@KRBSRV:~$ klist

    [OUTPUT]
    Ticket cache: FILE:/tmp/krb5cc_1000
    Default principal: ubuntu/admin@KRBSRV.LIN3

    Valid starting     Expires            Service principal
    12/08/22 16:53:32  12/09/22 02:53:32  krbtgt/KRBSRV.LIN3@KRBSRV.LIN3
            renew until 12/09/22 16:52:07
```

