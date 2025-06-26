# Sprint 1 - Intégration machines et utilisateurs

## Introduction

* [Samba et Microsoft, partage d'informations](https://linuxfr.org/news/accord-entre-le-projet-samba-et-microsoft)
* [Documentation de configuration de Samba](https://wiki.samba.org/index.php/Setting_up_Samba_as_an_Active_Directory_Domain_Controller)

## Objectif du sprint

Prérequis :  NTP doit être implémenté.

* Mise en place d'un AD et d'un DC sous Linux.

## Durée du sprint

A discuter avec les dev teams.

### Sprint Backlog

**Story 001 - Convention de nommage des machines (Business Value : 3 / Dev effort : 2)**

* Instance Windows -> ntpfailover.lin3.cpnv.ch
* Instance Debian -> ntpsrv.lin3.cpnv.ch
* Instance Ubunut -> dc.lin3.cpnv.ch

Note : aucun DNS ne doit être mis en place. Appuyez vous sur le fichier hosts locaux pour permettre aux machines de réaliser la résolution ip<->nom.

**Story 002 - Intégration d'un client (Windows et Linux) dans le domaine (Business Value : 3 / Dev effort : 2)**

**given**

* Le client n'est pas présent dans l'AD.

**when**

* Depuis le client, on lance la procédure d'intégration.

**then**

* Sur le serveur, on voit l'intégration du client.
* Après un reboot du client, on peut réaliser une authentification sur le domaine.

**Story 003 - Sortir un client (Windows et Linux) du domaine (Business Value : 3 / Dev effort : 2)**

**given**

* Le client est présent dans le domaine.

**when**

* Depuis le client, on lance la procédure pour sortir du domaine.

**then**

* Sur le serveur, on voit que le client n'est plus intégré.
* Après un reboot du client, on peut réaliser une authentification locale.

