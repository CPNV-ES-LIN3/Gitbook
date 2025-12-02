# Création d'images

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
