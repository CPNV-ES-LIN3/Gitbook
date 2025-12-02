# Kerberos Windows Client

Source [VM Ware](https://gpdb.docs.pivotal.io/6-7/admin_guide/kerberos-win-client.html#topic_win_kerberos_install)

TODO

* [ ] Download [MSI](http://web.mit.edu/kerberos/dist/kfw/4.0/kfw-4.0.1-amd64.msi)
* [ ] Run .msi executable

<figure><img src="../../../../../../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption></figcaption></figure>



* [ ] Set Local DNS
* [ ] Test DNS Resolution
* [ ] Set environment variables for the krb5.ini file(to the local config file)

{% hint style="info" %}
Get the /etc/krb5.conf file from your Linux Kerberos Server and rename it as "krb5.conf".

Place it in the installation folder of Kerberos
{% endhint %}

* [ ] Set cache for Kerberos
* [ ] Attempt to get a first ticket
* [ ] List the current cached tickets ([see issue](issue.md))
