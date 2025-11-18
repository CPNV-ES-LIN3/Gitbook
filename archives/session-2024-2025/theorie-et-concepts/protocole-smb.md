# Protocole SMB

## Introduction

L'intégration de **SMB (Server Message Block)** dans un environnement mixte Windows/Linux est un cas d'usage fréquent, surtout pour le partage de fichiers et d'imprimantes.

## **Accès aux Partages SMB Windows depuis Linux**

Linux peut accéder à des partages SMB/Windows directement, sans nécessiter Samba comme serveur, en utilisant des outils intégrés :

* **`mount -t cifs`** : Permet de monter un partage SMB sur un point de montage Linux.
* **`smbclient`** : Fonctionne comme un client FTP pour naviguer et interagir avec les partages SMB.

**Avantage :**

* Les systèmes Linux peuvent accéder aux ressources Windows sans configuration complexe.
* Pas besoin de déployer ou de maintenir un service Samba pour un simple accès client.

## **Interopérabilité avec les Protocoles SMB**

Linux utilise le **kernel CIFS module** pour interagir directement avec des partages SMB. Ce module prend en charge les versions modernes du protocole SMB (SMB 2.x, SMB 3.x), permettant :

* **Chiffrement des connexions** pour sécuriser les transferts.
* **Performances optimisées** grâce à SMB 3.x (compression, multicanaux, etc.).
* **Support des ACL** pour respecter les permissions définies sur les partages Windows.

**Avantage :** Une intégration native avec les infrastructures Windows modernes sans avoir à configurer un serveur Linux.

## **Gestion des Permissions et des Identités**

Même sans Samba, Linux peut gérer les permissions locales en mappant les identités AD :

* **SSSD (System Security Services Daemon)** :
  * Permet à Linux de se joindre à un domaine Active Directory.
  * Gère les utilisateurs et groupes AD pour les autorisations locales.
* **Winbind (optionnel)** :
  * Sans Samba serveur, Winbind peut encore être utilisé pour mapper les identités Windows aux comptes Linux.

**Avantage :** Maintien de la compatibilité avec les politiques AD pour des permissions cohérentes.

