# Kerberos Windows Client

Source [VM Ware](https://gpdb.docs.pivotal.io/6-7/admin_guide/kerberos-win-client.html#topic_win_kerberos_install)

* Download MSI

```
        [INPUT]
        wget http://web.mit.edu/kerberos/dist/kfw/4.0/kfw-4.0.1-amd64.msi -o kerberos.msi
        
        [OUTPUT]
        StatusCode        : 200
        StatusDescription : OK
        Content           : {208, 207, 17, 224...}
        RawContent        : HTTP/1.1 200 OK
                            X-Cnection: close
                            X-Pad: avoid browser bug
                            Connection: keep-alive
                            Content-Security-Policy: frame-ancestors 'self' https://web.mit.edu https://www.mit.edu
                            http://web.mit.edu http://...
          Headers           : {[X-Cnection, close], [X-Pad, avoid browser bug], [Connection, keep-alive],
                              [Content-Security-Policy, frame-ancestors 'self' https://web.mit.edu https://www.mit.edu
                              http://web.mit.edu http://www.mit.edu]...}
          RawContentLength  : 11034624
```

* Run .msi executable

<figure><img src="../../../../../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure>

* Set Local DNS

```
open C:\Windows\System32\drivers\etc\hosts

Add this line

10.0.2.11 KRBSRV.LIN3
```

* Test DNS Resolution

```
ping KRBSRV.LIN3

Pinging KRBSRV.LIN3 [10.0.2.11] with 32 bytes of data:
Reply from 10.0.2.11: bytes=32 time=1ms TTL=64
Reply from 10.0.2.11: bytes=32 time<1ms TTL=64

Ping statistics for 10.0.2.11:
    Packets: Sent = 2, Received = 2, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 1ms, Average = 0ms
```



* Set environment variables for the krb5.ini file(to local config file)

{% hint style="info" %}
Get the /etc/krb5.conf file from your Linux Kerberos Server and rename it as "krb5.conf".

Place it in the installation folder of Kerberos
{% endhint %}

```
set KRB5_CONFIG="C:\Program Files\MIT\Kerberos\krb5.ini"
```

* Set caching for Kerberos

```
set KRB5CCNAME=%USERPROFILE%\krb5cache
```

* Attempt to get a first ticket

```
[INPUT]
kinit testUser/admin

[OUTPUT]
Password for testUser/admin@KRBSRV.LIN3:***
```

* List current cached tickets&#x20;

```
[INPUT]
klist

[OUTPUT]
Current LogonId is 0:0x5ccef

Cached Tickets: (0)
```

{% hint style="info" %}
The prompt input doesn't show the ticket information, in despite the cache correctly reacting when kinit (create file) and kdestroy (delete file) are used.
{% endhint %}

<figure><img src="../../../../../.gitbook/assets/image (10) (1).png" alt=""><figcaption></figcaption></figure>

* Using the GUI Client, I assume that the caching is not the same as for the command line. Destroy ticket via commande line do not impact the GUI cache.

<figure><img src="../../../../../.gitbook/assets/image (9) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>
