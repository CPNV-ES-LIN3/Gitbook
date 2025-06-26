# PAM

{% embed url="https://www.cyberark.com/fr/what-is/privileged-access-management/" %}

## Introduction

L'utilisation de PAM (Pluggable Authentication Modules) dans un domaine avec un système centralisé comme Kerberos offre plusieurs avantages stratégiques et opérationnels.

## Intégration modulaire et flexible

PAM est conçu pour permettre une gestion modulaire de l'authentification. Cela signifie que vous pouvez configurer facilement différentes méthodes d'authentification, y compris Kerberos, sans nécessiter de modification dans les applications elles-mêmes. Les applications peuvent appeler PAM pour s'authentifier, et PAM s'occupe de la logique derrière, comme la validation via Kerberos.

* **Avantage** : Une flexibilité pour ajouter ou modifier des mécanismes d'authentification centralisés ou locaux (Kerberos, LDAP, ou autres).

## **Centralisation et Unicité de l'Authentification**

Dans un système basé sur Kerberos, l'objectif principal est de centraliser l'authentification pour tous les services et utilisateurs. PAM agit comme un pont entre les applications locales (par exemple, `sshd`, `sudo`, ou `login`) et Kerberos, permettant ainsi aux utilisateurs de s'authentifier une seule fois avec leurs identifiants Kerberos.

* **Avantage** :
  * Les utilisateurs n'ont pas besoin de gérer plusieurs identifiants.
  * L'intégration avec Kerberos via PAM simplifie la gestion des utilisateurs dans le domaine.

## **Support pour le Ticketing de Kerberos**

Kerberos repose sur un mécanisme de tickets (TGT - Ticket Granting Ticket). PAM peut être configuré pour gérer automatiquement ces tickets lors de l'authentification. Par exemple, lors de la connexion via SSH, PAM peut non seulement valider l'utilisateur, mais aussi initier un TGT pour que l'utilisateur puisse accéder à d'autres services sans se réauthentifier.

* **Avantage** : Un Single Sign-On (SSO) fluide dans le domaine, augmentant la productivité et la convivialité.

## **Gestion Uniforme des Politiques d'Authentification**

PAM centralise la gestion des politiques d'authentification pour les services locaux. En intégrant Kerberos, il devient possible de configurer des règles globales (par exemple, des limitations de mot de passe ou des restrictions d'accès) qui s'appliquent uniformément à travers tout le domaine.

* **Avantage** :
  * Renforcement de la sécurité grâce à des politiques cohérentes.
  * Réduction des risques d'erreurs de configuration sur des services individuels.

## **Compatibilité avec des Environnements Hybrides**

Dans certains environnements, tous les systèmes ou services ne sont pas intégrés à Kerberos. PAM permet d'utiliser Kerberos pour certains services tout en utilisant d'autres mécanismes pour des services non intégrés (comme l'authentification locale ou via un autre annuaire).

* **Avantage** : Une gestion progressive et adaptable vers une migration complète ou une cohabitation sans rupture

## **Séparation des Responsabilités et Maintenance Facile**

PAM sépare la gestion de l'authentification (gérée par PAM) de celle des applications ou des services (comme `sshd` ou `su`). Avec Kerberos intégré via PAM, il devient plus simple de maintenir et mettre à jour le système d'authentification centralisé sans avoir à modifier chaque service.

* **Avantage** : Réduction de la charge de maintenance et des risques associés aux changements.
