# Docker et la sécurité

## Introduction

La virtualisation avec Docker apporte de nombreux avantages en termes de déploiement et de gestion d'applications, mais elle introduit également des préoccupations spécifiques en matière de sécurité.&#x20;

Voici quelques points clés à considérer :

## **Isolation des Conteneurs**

* **Isolation par Namespace :** <mark style="color:orange;">Docker utilise des namespaces Linux</mark> pour isoler les conteneurs entre eux. Cependant, <mark style="color:orange;">cette isolation n'est pas aussi robuste qu'une isolation complète offerte par les machines virtuelles</mark>. Les failles de sécurité dans le noyau peuvent potentiellement permettre à un attaquant de sortir d'un conteneur et d'accéder à l'hôte ou à d'autres conteneurs.
* **Isolation par Cgroups :** Les cgroups (control groups) <mark style="color:orange;">limitent l'utilisation des ressources</mark> par les conteneurs, mais ils ne fournissent pas une isolation complète, notamment au niveau de l'utilisation des ressources matérielles.

<figure><img src="../../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

Source : [Medium](https://medium.com/@mrdevsecops/namespace-vs-cgroup-60c832c6b8c8)

## **Accès Root et Privilèges Élevés**

* **Conteneurs en tant que Root :** <mark style="color:orange;">Par défaut, les processus à l'intérieur d'un conteneur sont exécutés en tant que root</mark>, ce qui peut être problématique si un conteneur est compromis. Un attaquant pourrait potentiellement obtenir des privilèges élevés sur l'hôte.
* **Capability Dropping :** Docker permet de réduire les capacités (capabilities) d'un conteneur pour minimiser les privilèges. <mark style="color:orange;">C’est une bonne pratique de retirer toutes les capacités non nécessaires</mark>.

## **Sécurité du Kernel**

* **Surface d'attaque du Kernel :** Docker <mark style="color:orange;">partage le même noyau avec l'hôte et les autres conteneurs</mark>. Une vulnérabilité dans le noyau Linux pourrait être exploitée pour attaquer l'hôte ou d'autres conteneurs.

<figure><img src="../../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## **Sécurité des Images**

* **Images Compromises :** <mark style="color:orange;">Les images Docker peuvent contenir des logiciels vulnérables ou malveillants</mark>. Il est essentiel de télécharger des images uniquement à partir de sources fiables et de scanner les images pour des vulnérabilités.
* **Politique d'Images Signées :** Docker prend en charge la signature d'images (<mark style="color:orange;">Docker Content Trust</mark>), ce qui permet de vérifier l'intégrité et l'authenticité des images avant de les déployer.

<figure><img src="../../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

## **Réseautage et Communication**

* **Isolation Réseau :** Par défaut, tous les conteneurs sur le même hôte peuvent communiquer entre eux via le réseau bridge de Docker. Il est important de configurer des réseaux personnalisés ou d'utiliser des solutions comme `docker network` pour limiter la communication inter-conteneurs.
* **Exposition des Ports :** Les ports ouverts par les conteneurs peuvent être des points d'entrée pour des attaques. Il est crucial de n'exposer que les ports nécessaires et d'utiliser des pare-feux ou des reverse proxies pour contrôler l'accès.

<figure><img src="../../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

Source : [DevToDevops](https://devtodevops.com/docker-network-overlay-vs-bridge/)



## **Mises à Jour et Gestion des Patches**

* **Patching Régulier :** Comme tout logiciel, Docker et le système d'exploitation sous-jacent nécessitent des mises à jour régulières pour corriger les vulnérabilités.
* **Vulnérabilités dans les Dépendances :** Les images Docker peuvent contenir de nombreuses dépendances. Il est important de les maintenir à jour et de les reconstruire régulièrement.

<figure><img src="../../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>



## **Attaques et Menaces**

* **Conteneurs Malveillants :** Si un attaquant parvient à insérer un conteneur malveillant sur un hôte, il pourrait potentiellement attaquer d'autres conteneurs ou l'hôte lui-même.
* **DDoS et Overcommitment :** Un conteneur peut consommer excessivement les ressources (CPU, mémoire) si les limites ne sont pas correctement définies, provoquant des dégradations de performance ou un déni de service.

<figure><img src="../../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

## **Pratiques de Sécurité Recommandées**

* **Utiliser SELinux ou AppArmor :** Ces modules de sécurité renforcent l'isolation des conteneurs.
* **Moins de Privileges :** Exécuter les conteneurs avec des utilisateurs non root lorsque c’est possible.
* **Surveiller et Scanner les Conteneurs :** Utiliser des outils comme Docker Bench for Security, Clair, ou Aqua pour surveiller et scanner les conteneurs en temps réel.

<figure><img src="../../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

## Conclusion

{% hint style="warning" %}
En résumé, bien que Docker fournisse des mécanismes pour la sécurité, il est crucial de bien comprendre les limites de ces mécanismes et de mettre en place des stratégies de sécurité supplémentaires pour protéger les systèmes utilisant Docker.
{% endhint %}
