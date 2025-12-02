# Sprint 1 - La gestion du temps

## Objectif du sprint

Implémenter le protocole NTP.

**Exemple d'une infrastructure cible.**

![Infrastructure](<../../../../.gitbook/assets/image (6) (1) (1).png>)

## Durée du sprint

A discuter avec les dev teams.

### Sprint 01 - Mise en place d'un système de synchronisation d'horloge

**Story 001 - Acquisition de compétence théorique (Business Value : 3 / Dev effort : 2)**

* [Wikipedia](https://fr.wikipedia.org/wiki/Network_Time_Protocol)
* [NTP.orp](http://support.ntp.org/bin/view/Main/WebHome)
* [Frameip.com](https://www.frameip.com/ntp/)
* [Serveurs sources US ](https://tf.nist.gov/tf-cgi/servers.cgi) / [Serveurs sources UK](https://www.pool.ntp.org/vendors.html)&#x20;

Voici les points qui doivent être étudiés (liste non exaustive):

* Quels types d'architectures propose NTP ?
* Quels sont les composants du NTP (en plus de l'horloge atomique) ?
* Comment les serveurs NTP se protègent d'éventuelles attaques (à quoi devez-vous faire attention lors de l'implémentation) ?
* Selon la configuration standard de NTP, un client est-il également un serveur potentiel ?
* Ports, protocoles utilisés par le NTP ?
* Objectif du NTP ?
* SNTP ?
* Fuseau horaire et NTP ?
* Comment choisir le bon client NTP ?

**Story 002 - Mettre en place son propre serveur source directement derrière une horloge atomique de notre choix (Business Value : 5 / Dev effort : 1)**

Description : L'instance SSH synchronise son temps avec&#x20;

* time-d-b.nist.gov (primaire)
* utcnist2.colorado.edu (secondaire)

Note : horloges atomiques à adapter en fonction du positionnement géographique de notre propre serveur de temps.

**given**

* Je suis connecté sur l'instance SSH.
* Je modifie l'heure système.

**when**

* Je lance (force) une synchronisation.

**then**

* Le log du ntp mentionne les interactions avec les horloges sources.
* Le temps est à nouveau synchronisé.
* Je vérifie le fuseau horaire. Il s'agit bien de celui de Zürich.

**Story 003 - Mettre en place un client NTP se connectant à notre serveur source (Business Value : 5 / Dev effort : 3)**

Description : l'instance Domain Controler synchronise son temps avec l'instance SSH

**given**

* Je suis connecté sur l'instance Domain Controler.
* Je modifie l'heure.
* Je démontre que les horloges sources sont bien celles mentionnées.
* Je montre le pare-feu activé et l'exception qui a été ajoutée pour permettre aux clients de synchroniser leur horloge.

**when**

* Je lance (force) une synchronisation.

**then**

* Le log du ntp mentionne les interactions avec les horloges sources.
* Le temps est à nouveau synchronisé.
* Je démontre que les horloges sources sont bien celles mentionnées.
* NTP est bien un service (persistence après un redémarrage).

## **En savoir plus**

**Story 004 - Sécuriser son serveur NTP (Business Value : 5 / Dev Effort : 4)**

Description : Sécuriser son serveur NTP

{% embed url="https://Redhat.com" %}

**Story 005 - Paramétrages avancés de NTP**

[DriftFile](https://osr507doc.xinuos.com/en/NetAdminG/ntpC.driftfile.html)

[LeapFile](https://kb.meinbergglobal.com/kb/time_sync/ntp/configuration/ntp_leap_second_file)

[Statistics](http://doc.ntp.org/4.2.4/monopt.html)

### En savoir plus

[Network Time Security](https://www.netnod.se/blog/everything-you-need-know-about-network-time-security)
