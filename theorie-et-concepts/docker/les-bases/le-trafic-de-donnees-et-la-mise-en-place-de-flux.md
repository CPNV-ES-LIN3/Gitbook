# Le trafic de données et la mise en place de flux

Le trafic de données et la mise en place de flux entre différents conteneurs Docker peuvent être expliqués en s'appuyant sur les concepts fondamentaux du réseau Docker.&#x20;

Voici une explication étape par étape :

## **Isolation des Conteneurs**

* **Conteneurs** : Chaque conteneur Docker fonctionne de manière isolée avec son propre environnement, comprenant un système de fichiers, un réseau, et d'autres ressources. Cependant, <mark style="color:orange;">les conteneurs peuvent communiquer entre eux via le réseau Docker</mark>.
* **Namespaces** : Docker utilise les "namespaces" pour créer cette isolation, y compris le "<mark style="color:orange;">network namespace</mark>", qui permet à chaque conteneur d'avoir sa propre pile réseau.

## **Réseaux Docker**

* Docker crée <mark style="color:orange;">un réseau par défaut</mark> pour les conteneurs, appelé <mark style="color:orange;">**bridge network**</mark>. Lorsque plusieurs conteneurs sont attachés à un même réseau bridge, <mark style="color:orange;">ils peuvent se communiquer directement en utilisant leurs adresses IP internes</mark>.
* **Bridge Network** : Ce réseau <mark style="color:orange;">permet à des conteneurs sur la même machine hôte de communiquer entre eux</mark>. Par défaut, les conteneurs peuvent utiliser le nom d'hôte ou l'adresse IP du conteneur cible pour envoyer des requêtes.
* **Custom Networks** : Vous pouvez créer des <mark style="color:orange;">réseaux personnalisés</mark> (comme un bridge personnalisé), où les conteneurs peuvent se trouver sur le même sous-réseau, ce qui facilite leur communication.

## **Gestion des Ports**

* **Ports Exposés** : <mark style="color:orange;">Pour qu'un service à l'intérieur d'un conteneur soit accessible de l'extérieur</mark>, il faut <mark style="color:orange;">exposer un port du conteneur</mark>. Docker permet de mapper un port du conteneur à un port de la machine hôte, ce qui rend le service accessible depuis l'extérieur (ex : `-p 8080:80`).
* **Ports Internes** : <mark style="color:orange;">Les conteneurs peuvent aussi communiquer entre eux via des ports internes</mark> (non exposés à l'extérieur), ce qui est souvent utilisé pour des microservices qui s'interconnectent sur des réseaux internes.

## **Communication entre Conteneurs**

* **Nom de Service** : Lorsqu'un conteneur est connecté à un réseau, il peut être <mark style="color:orange;">accédé par son nom d'hôte</mark>, ce qui rend la communication plus simple et ne dépend pas des adresses IP (qui peuvent changer).
* **Docker Compose** : Avec <mark style="color:orange;">Docker Compose, vous pouvez définir un ensemble de conteneurs et de réseaux</mark>, ce qui facilite la mise en place de communications entre eux. Les conteneurs d'un même `docker-compose.yml` peuvent se voir mutuellement par leur nom de service.

## **Mise en Place de Flux**

* **Services** : Les conteneurs peuvent être configurés pour exécuter différents services (comme une <mark style="color:orange;">base de données, un serveur web</mark>, etc.). En connectant ces conteneurs via un réseau Docker, les services peuvent échanger des données.
* **Flux de Données** : Par exemple, <mark style="color:orange;">un conteneur</mark> exécutant une application web <mark style="color:orange;">peut envoyer des requêtes à un conteneur de base de données</mark> pour récupérer des informations, traiter ces données, puis retourner les résultats via un serveur web.
* **Volume** : Pour le stockage de données partagées, vous pouvez <mark style="color:orange;">utiliser des volumes Docker</mark>, qui permettent à <mark style="color:orange;">plusieurs conteneurs de lire et écrire sur le même système de fichiers partagé</mark>.

## **Réseau Overlay pour Multihost**

* Pour des environnements où les conteneurs sont répartis sur plusieurs hôtes, Docker Swarm ou <mark style="color:orange;">Kubernetes</mark> utilisent des **réseaux overlay** qui permettent la communication sécurisée entre les conteneurs sur différents hôtes en créant <mark style="color:orange;">un réseau virtuel distribué</mark>.

