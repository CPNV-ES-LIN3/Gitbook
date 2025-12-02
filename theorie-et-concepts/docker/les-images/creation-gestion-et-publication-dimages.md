# Création, gestion et publication d'images

## Introduction

Docker est un outil de conteneurisation qui permet aux développeurs de <mark style="color:orange;">créer, tester et déployer</mark> des applications rapidement. Un des éléments centraux de Docker est <mark style="color:orange;">l'image, qui représente un modèle immuable contenant tout ce qui est nécessaire pour exécuter une application</mark> :&#x20;

* le code,&#x20;
* les bibliothèques,&#x20;
* les variables d'environnement, et&#x20;
* les configurations par défaut.

## **Création d'images**

### **Dockerfile**

Un Dockerfile est un script texte qui contient une série d'instructions pour assembler une image Docker. Chaque ligne du Dockerfile représente une commande qui sera exécutée pour créer l'image. Par exemple, l'instruction `FROM` spécifie l'image de base, tandis que `RUN` permet d'exécuter une commande dans le conteneur.

```docker
# syntax=docker/dockerfile:1

FROM node:18-alpine             //image de base
WORKDIR /app                    //chemin de travail appliqué aux prochaines commmandes
COPY . .                        //copie du local vers l'image ( "." = emplacement actuel)
RUN yarn install --production   //installation des dépendances avec yarn
CMD ["node", "src/index.js"]    //on utilise l'exécutable node pour lire le fichier index.js
EXPOSE 3000                     //mentionner que l'image va exposer le 3000
```

### **Build d'une image**

La commande `docker build` permet de <mark style="color:orange;">créer une image à partir d'un Dockerfile</mark>. Il est essentiel de suivre les bonnes pratiques lors de la rédaction du Dockerfile pour optimiser la taille de l'image et la vitesse de construction.

```docker
docker build -t getting-started .
```

{% embed url="https://docs.docker.com/build/building/best-practices/" %}

{% embed url="https://docs.docker.com/build/" %}

### **Gestion des couches**&#x20;

Docker utilise un système de couches (layers) pour construire ses images. Chaque instruction dans le Dockerfile crée une nouvelle couche dans l'image. Il est important de minimiser le nombre de couches pour réduire la taille finale de l'image.

{% hint style="warning" %}
Combien de layer(s) ce docker file va-t-il produire ?
{% endhint %}

```docker
# syntax=docker/dockerfile:1
FROM ubuntu:22.04

# install app dependencies
RUN apt-get update && apt-get install -y python3 python3-pip
RUN pip install flask==3.0.*

# install app
COPY hello.py /

# final configuration
ENV FLASK_APP=hello
EXPOSE 8000
CMD ["flask", "run", "--host", "0.0.0.0", "--port", "8000"]
```

{% embed url="https://youtu.be/wJwqtAkmtQA" %}

## Gestion des images

#### **Optimisation de la taille des images**

Pour réduire la taille des images Docker, utilisez des images de base légères comme `alpine`, nettoyez les caches des gestionnaires de paquets (`apt-get clean`), et combinez les instructions du Dockerfile pour minimiser le nombre de couches.



**Tagging des images**

Lors de la construction d'une image, il est recommandé d'utiliser des tags explicites pour identifier les versions (par exemple, `myapp:1.0.0`). Les tags permettent de gérer facilement les différentes versions d'une image.

#### **Sécurité des images**

Utilisez des images de sources fiables et vérifiez régulièrement les vulnérabilités. Docker propose des outils comme `docker scan` pour analyser les images en local et identifier les vulnérabilités de sécurité.

#### **Nettoyage régulier**

Utilisez les commandes `docker system prune` et `docker image prune` pour nettoyer les images inutilisées et éviter l'encombrement du disque dur local.

#### **Cohérence entre les environnements**

Assurez-vous que les images utilisées en développement sont les mêmes que celles déployées en production. Cela garantit que l'application se comportera de la même manière dans les deux environnements.

## Publication d'images

**Docker Hub et autres registres**

Docker Hub est le <mark style="color:orange;">registre d'images public</mark> le plus utilisé, mais il existe aussi des alternatives comme GitHub Container Registry, Amazon ECR, <mark style="color:orange;">ou des registres privés</mark>. Publier une image sur un registre permet de la partager avec d'autres équipes ou de la déployer sur différents environnements.

**Tagging et versionnement**

Avant de publier une image, il est crucial de lui attribuer un <mark style="color:orange;">tag significatif</mark> qui inclut souvent un numéro de version (par exemple, `myapp:1.2.3`). Cela permet de gérer les mises à jour et de maintenir la compatibilité.

{% embed url="https://docs.docker.com/reference/cli/docker/image/tag/" %}

### **Sécurité**

Assurez-vous que l'<mark style="color:orange;">image ne contient pas d'informations sensibles avant de la publier</mark>. Cela inclut des secrets, des clés API, ou des configurations spécifiques à l'environnement local.

#### **Automatisation de la publication**

Vous pouvez automatiser la construction et la publication des images avec des outils CI/CD comme Jenkins, GitLab CI, ou GitHub Actions. Cela garantit une intégration continue et des déploiements automatisés avec la dernière version de l'image.

<figure><img src="../../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

Source : [Redhat](https://www.redhat.com/en/topics/devops/what-is-ci-cd)

#### **Documentation**

Fournissez une documentation claire pour chaque image publiée, y compris les instructions d'utilisation, les variables d'environnement configurables, et les prérequis. Une bonne documentation facilite l'adoption et l'utilisation correcte de l'image.

{% embed url="https://hub.docker.com/_/nginx" %}

## Conclusion

La gestion des images Docker implique une attention particulière à la construction, à l'optimisation et à la sécurité des images. Les bonnes pratiques incluent l'utilisation efficace des Dockerfile, le nettoyage régulier des images locales, et le respect des standards de sécurité lors de la publication sur des registres publics. En automatisant les processus de construction et de publication, vous assurez une livraison rapide et fiable des applications à travers différents environnements.
