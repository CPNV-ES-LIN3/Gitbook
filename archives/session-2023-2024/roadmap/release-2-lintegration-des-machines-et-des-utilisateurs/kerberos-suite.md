# Sprint 1 - Intégration machines et utilisateurs

## Objectif du sprint

Prérequis :  NTP doit être implémenté tout comme Kerberos.

* Intégration des clients linux et windows dans le domaine.
* Gérer le domaine linux sur le serveur.

## Durée du sprint

A discuter avec les dev teams.

### Sprint Backlog

**Story 001 - Convention de nommage des machines (Business Value : 3 / Dev effort : 2)**

* Instance Windows -> win-cli.\[mondomaine]
* Instance Debian -> lin-cli.\[mondomaine]
* Instance CentOs -> lin-dc.\[mondomaine]

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

