# Sprint 2 - Authentification

## Objectif du sprint

Prérequis :  NTP doit être implémenté.

Mise en place de Kerberos.

## Durée du sprint

A discuter avec les dev teams.

## Sprint Backlog

**Story 001 - Acquisition de compétences théorique (Business Value : X / Dev effort : X)**

Sources à étudier:

* [Kerberos - Principes de bases](sprint-2-authentification.md#objectif-du-sprint)
* [Kerberos - MIT](https://web.mit.edu/kerberos/krb5-latest/doc/) (documentation qui sera à disposition durant les examens)&#x20;

{% embed url="https://www.youtube.com/watch?v=5N242XcKAsM" %}



* Les composants logiques de Kerberos.
* Objectif de Kerberos.
* NTP et Kerberos ?
* Kerberos est un domaine Windows ?

**Story 002 - Mise en place du serveur Kerberos (Business Value : X / Dev effort : X)**

Description : il s'agit de mettre en place sur Linux un serveur Kerberos

**Critères d'acceptation**:

* OS du serveur : Debian 11
* Paramètrage domaine : \[groupename].actualit.info
* Kerberos est un service.
* Mise à jour du pare-feu pour autoriser les futurs clients.
* Les instances de la DMZ ne doivent pas réussir à obtenir un ticket.
* Mise à jour du schéma de l'infrastructure.

Note : DNS. Dans un premier temps, l'utilisation des fichiers hosts est conseillée (dépendance AWS)

**Story 003 - Connection à Kerberos depuis un Client Windows (Business Value : X / Dev effort : X)**

Description : il s'agit &#x64;**'**&#x6F;btenir un ticket depuis le client windows

**Critères d'acceptation**:

* OS du client W2k22
* Mise à jour du pare-feu du client
* On obtient un ticket sur le client
* On observe l'ouverture du ticket sur le serveur Kerberos
* Script de configuration disponible&#x20;

Note : DNS. Dans un premier temps, l'utilisation des fichiers hosts est conseillée (dépendance AWS)

**Story 004 - Connection à Kerberos depuis un Client Linux (Business Value : X / Dev effort : X)**

Description : il s'agit &#x64;**'**&#x6F;btenir un ticket depuis le client windows

**Critères d'acceptation**:

* OS du client Ubuntu 20.04
* Mise à jour du pare-feu du client
* On obtient un ticket sur le client
* On observe l'ouverture du ticket sur le serveur Kerberos
* Script de configuration disponible

Note : DNS. Dans un premier temps, l'utilisation des fichiers hosts est conseillée (dépendance AWS)

**Story 005 - Désynchronisation des horloges (Business Value : X / Dev effort : X)**

Description : il s'agit d'experimenter une erreur Kerberos en lien avec une différence de temps entre client et serveur Kerberos &#x20;

**Critères d'acceptation**:

* Identifier dans la configuration Kerberos la tolérance en lien avec la différence d'horloge
* Depuis un client Windows ou Linux (présentant une désynchronisation d'horloge)
* Tentative de demande de ticket
* Erreur retournée par le serveur
* Script de configuration disponible&#x20;

Note : DNS. Dans un premier temps, l'utilisation des fichiers hosts est conseillée (dépendance AWS)

