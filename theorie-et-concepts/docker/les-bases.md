# Les bases

## Introduction

{% embed url="https://youtu.be/0qotVMX-J5s" %}

## Comparaisons entre VM et les conteneurs

{% embed url="https://youtu.be/a1M_thDTqmU" %}

## Comparaison entre la virtualisation basée sur des machines virtuelles et la contenerisation

Les différences majeures entre la virtualisation basée sur des machines virtuelles (VM) et la conteneurisation sont les suivantes :

1. **Isolation** : Les machines virtuelles offrent une isolation complète en incluant <mark style="color:orange;">un système d'exploitation entier pour chaque VM</mark>, tandis que <mark style="color:orange;">la conteneurisation partage le même noyau du système d'exploitation hôte</mark>, ce qui permet aux conteneurs d'être plus légers.
2. **Performance** : <mark style="color:orange;">Les conteneurs sont généralement plus performants que les VM car ils consomment moins de ressources</mark>, démarrent plus rapidement, et utilisent moins de mémoire et de stockage, grâce à l'absence de système d'exploitation dédié par conteneur.
3. **Portabilité** : Les conteneurs sont plus portables que les VM puisqu<mark style="color:orange;">'ils incluent uniquement les dépendances nécessaires pour exécuter les applications</mark>, ce qui permet de les déplacer facilement entre différents environnements sans modifications majeures.
4. **Gestion des ressources** : <mark style="color:orange;">Les VM nécessitent des hyperviseurs</mark> pour gérer les ressources matérielles et créer des environnements virtuels distincts, alors que <mark style="color:orange;">la conteneurisation utilise des moteurs comme Docker</mark> pour exécuter des conteneurs, offrant une gestion plus efficace des ressources.
5. **Cas d'usage** : <mark style="color:orange;">Les machines virtuelles sont souvent utilisées pour des environnements qui nécessitent une isolation forte ou des systèmes d'exploitation différents</mark>, tandis que <mark style="color:orange;">les conteneurs sont préférés pour les déploiements d'applications légères</mark>, les microservices et les environnements de développement où la rapidité et la portabilité sont cruciales.

## D'un point de vue de l'architecture

Source : [Net Solutions](https://www.netsolutions.com/insights/containerization-vs-virtualization/)

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Observations:

* L'hyperviseur intègre son propre système d'exploitation alors que le "container engine" partage les propriétés de virtualisation offertes par l'OS (linux).

{% hint style="warning" %}
Avec Docker, sommes-nous en présence d'une architecture qui ressemble plus a un hyperviseur de type I ou II ?
{% endhint %}
