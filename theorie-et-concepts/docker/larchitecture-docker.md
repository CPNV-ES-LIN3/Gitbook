# L'architecture Docker

## Overview

"Docker est une <mark style="color:orange;">plateforme libre</mark> faite pour <mark style="color:orange;">le développement, le déploiement et l'exécution d'applications</mark>. Docker vous permet de séparer vos applications de votre infrastructure afin de fournir rapidement des logiciels.&#x20;

Avec Docker, vous pouvez <mark style="color:orange;">gérer votre infrastructure de la même manière que vos applications</mark>. En tirant parti des méthodologies de Docker pour le developpement, le test et le déploiement du code, vous pouvez <mark style="color:orange;">réduire considérablement le délai entre l'écriture du code et son exécution en production</mark>."

## The Docker platform

"Docker permet d'empaqueter (package) et d'exécuter une application dans un environnement faiblement isolé appelé conteneur.&#x20;

L'isolation et la sécurité permettent d'exécuter simultanément de nombreux conteneurs sur un hôte donné.&#x20;

Les conteneurs sont légers et contiennent tout ce qui est nécessaire à l'exécution de l'application, de sorte que vous n'avez pas besoin de vous fier à ce qui est installé sur l'hôte.&#x20;

Vous pouvez partager des conteneurs pendant que vous travaillez, et être sûr que toutes les personnes avec lesquelles vous partagez obtiennent le même conteneur qui fonctionne de la même manière."

<mark style="color:orange;">Docker fournit des outils et une plateforme pour gérer le cycle de vie de vos conteneurs</mark> :

Développez votre application et ses composants à l'aide de conteneurs.&#x20;

Le conteneur devient l'<mark style="color:orange;">unité de distribution et de test</mark> de votre application.&#x20;

Lorsque vous êtes prêt, déployez votre application dans votre environnement de production, en tant que <mark style="color:orange;">conteneur</mark> ou <mark style="color:orange;">service orchestré</mark>.&#x20;

## Docker architecture

Source : [Docker](https://docs.docker.com/guides/docker-overview/)

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

<table><thead><tr><th width="166">Composant</th><th>Rôle dans l'achitecture</th></tr></thead><tbody><tr><td>Client</td><td>Est le moyen le plus simple de dialoguer avec le "daemon docker". Via une api, vous pouvez lui demander d'exécuter les commandes et ainsi gérer le cycle de vie des conteneurs.</td></tr><tr><td>Docker Host</td><td>Est constitué de différents composants:<br><br>* le docker daemon, qui est le service principal qui exécute les commandes et maintient l'état des conteneurs<br><br>* les images, qui sont l'équivalent des "iso" des machines virtuelles d'une certaines manière. Elle seront utiles pour construire des conteneurs.<br><br>* les conteneurs, qui sont le résultat des images après construction (build) et qui peuvent être dans différents états.</td></tr><tr><td>Registry</td><td>Sert de bibliothèque d'images privés ou publiques. DockerHub en est un exemple publique. Cela permet à la communauté de s'échanger des images et d'avoir un référentiel commun.</td></tr></tbody></table>
