# Monitoring et Docker

## Introduction

La **surveillance (monitoring) d'une infrastructure Docker** est essentielle pour <mark style="color:orange;">garantir la stabilité, la performance et la sécurité des applications conteneurisées</mark>. Docker étant une solution très populaire pour la conteneurisation, il est important de suivre plusieurs aspects spécifiques liés à cette technologie.

## Les différentes sources de données (métriques)

<figure><img src="../../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

<p align="center">Source : <a href="https://cloud.google.com/blog/products/operations/in-depth-explanation-of-operational-metrics-at-google-cloud">Google Cloud Monitoring</a></p>

### Surveillance de l'hôte Docker

<mark style="color:orange;">L'hôte (ou serveur physique/virtuel qui exécute Docker)</mark> est essentiel à la santé des conteneurs. Les métriques importantes à surveiller incluent :

* <mark style="color:orange;">**Utilisation du CPU**</mark> : Vérifier si l'hôte est surchargé et si les conteneurs reçoivent suffisamment de ressources.
* <mark style="color:orange;">**Utilisation de la mémoire RAM**</mark> : Suivre la consommation de mémoire pour s'assurer qu'il n'y ait pas de saturation.
* <mark style="color:orange;">**Espace disque**</mark> : Docker consomme beaucoup d'espace disque pour stocker les images, les volumes et les logs.
* <mark style="color:orange;">**Performances du réseau**</mark> : Suivre le trafic réseau pour détecter d'éventuels goulets d'étranglement.

### Surveillance des conteneurs

* **Utilisation des ressources des conteneurs** : Vérifier la <mark style="color:orange;">consommation de CPU, de mémoire et de disque par chaque conteneur individuellement</mark>.
* **Disponibilité des services** : S'assurer que les applications déployées dans les conteneurs sont <mark style="color:orange;">accessibles</mark> et fonctionnelles.
* **Événements Docker** : Par exemple, si u<mark style="color:orange;">n conteneur redémarre fréquemment</mark>, il est important d'analyser pourquoi cela se produit.

## Logs des conteneurs

<figure><img src="../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

Source : Capture d'écran de Datadog - [middelware.io](https://middleware.io/blog/what-is-log-monitoring/)

### Logs d'application

Les logs des services exécutés à l'intérieur des conteneurs doivent être surveillés pour <mark style="color:orange;">détecter les erreurs ou comportements anormaux</mark>.

<figure><img src="../../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

<p align="center">Exemple de log produit par Apache</p>

### Logs Docker

<mark style="color:orange;">Docker produit ses propres logs</mark> qui peuvent révéler des informations précieuses sur l’état du système.

<figure><img src="../../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>
