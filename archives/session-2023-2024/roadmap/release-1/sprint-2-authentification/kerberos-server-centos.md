# Kerberos Server - CentOS

## Kerberos Server Setup

### Infra

* Kerberos Server : CentOS
* Kerberos Lin Client : Debian 12
* Kerberos Win Client : W2k22

### Kerberos Server Setup

[Installation Guide](https://ubuntu.com/server/docs/service-kerberos)

[Kadmin Guide](https://web.mit.edu/kerberos/krb5-1.12/doc/admin/admin_commands/kadmin_local.html)

* Config Kerberos

{% hint style="info" %}
REAL: KRBSRV.LIN3
{% endhint %}

### TODO - Initial setup

* [ ] Set Kerberos Admin Server as a service
* [ ] Set Keberos KDC as a service
* [ ] Create Kerberos Database
* [ ] Create an admin for Kerberos Administration
* [ ] Update ACL for this new user
* [ ] Fix the hostname and make it persistent [AWS Guide](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/set-hostname.html)

### TODO - Validation

* [ ] Ask ticket
* [ ] Get ticket details

