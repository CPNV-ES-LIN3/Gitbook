# Les bases

## Introduction

{% embed url="https://youtu.be/0qotVMX-J5s" %}

## Comparaisons entre VM et les conteneurs

{% embed url="https://youtu.be/a1M_thDTqmU" %}

## Rôle de l'hyperviseur

"Un hyperviseur est un <mark style="color:orange;">logiciel</mark> qui permet la création et la gestion de machines virtuelles (VM) sur un <mark style="color:orange;">hôte physique</mark>. Il <mark style="color:orange;">divise les ressources matérielles de l'hôte</mark>, comme le processeur, la mémoire et le stockage, et les distribue entre plusieurs VM, tout en assurant leur <mark style="color:orange;">isolation</mark>. L'hyperviseur gère également l'<mark style="color:orange;">exécution</mark> des VM, s'assurant qu'elles fonctionnent efficacement <mark style="color:orange;">sans interférer</mark> les unes avec les autres. Il existe deux types principaux d'hyperviseurs : les hyperviseurs de <mark style="color:orange;">type 1</mark>, qui s'exécutent directement sur le matériel, et les hyperviseurs de <mark style="color:orange;">type 2</mark>, qui fonctionnent au-dessus d'un système d'exploitation hôte. Le rôle principal de l'hyperviseur est de <mark style="color:orange;">maximiser l'utilisation des ressources matérielles</mark> et d'assurer la flexibilité, la scalabilité et la sécurité des environnements virtuels."

## Hyperviseur type I et II

Les hyperviseurs de type I et II se distinguent principalement par leur mode de fonctionnement et leur <mark style="color:orange;">interaction avec le matériel</mark>.

1. **Type I (Bare-Metal Hypervisor)** : Ce type d'hyperviseur fonctionne <mark style="color:orange;">directement sur le matériel physique de l'hôte</mark>, sans passer par un système d'exploitation intermédiaire. En raison de cette proximité avec le matériel, les hyperviseurs de type I offrent généralement de <mark style="color:orange;">meilleures performances</mark>, une plus grande efficacité et une sécurité renforcée. Ils sont couramment utilisés dans les environnements de serveurs et de <mark style="color:orange;">centres de données</mark>.
2. **Type II (Hosted Hypervisor)** : L'hyperviseur de type II s'exécute <mark style="color:orange;">au-dessus d'un système d'exploitation hôte</mark>, comme une application logicielle. Il est plus simple à installer et à utiliser, ce qui le rend populaire pour les tests, le développement, ou pour exécuter plusieurs systèmes d'exploitation sur des ordinateurs personnels. Cependant, il peut être moins performant que le type I en raison de la couche supplémentaire du système d'exploitation hôte.

Source:  [AWS](https://aws.amazon.com/compare/the-difference-between-type-1-and-type-2-hypervisors/)

## Comparaison entre la virtualisation basée sur des machines virtuelles et la contenerisation

Les différences majeures entre la virtualisation basée sur des machines virtuelles (VM) et la conteneurisation sont les suivantes :

1. **Isolation** : Les machines virtuelles offrent une isolation complète en incluant <mark style="color:orange;">un système d'exploitation entier pour chaque VM</mark>, tandis que <mark style="color:orange;">la conteneurisation partage le même noyau du système d'exploitation hôte</mark>, ce qui permet aux conteneurs d'être plus légers.
2. **Performance** : <mark style="color:orange;">Les conteneurs sont généralement plus performants que les VM car ils consomment moins de ressources</mark>, démarrent plus rapidement, et utilisent moins de mémoire et de stockage, grâce à l'absence de système d'exploitation dédié par conteneur.
3. **Portabilité** : Les conteneurs sont plus portables que les VM puisqu<mark style="color:orange;">'ils incluent uniquement les dépendances nécessaires pour exécuter les applications</mark>, ce qui permet de les déplacer facilement entre différents environnements sans modifications majeures.
4. **Gestion des ressources** : <mark style="color:orange;">Les VM nécessitent des hyperviseurs</mark> pour gérer les ressources matérielles et créer des environnements virtuels distincts, alors que <mark style="color:orange;">la conteneurisation utilise des moteurs comme Docker</mark> pour exécuter des conteneurs, offrant une gestion plus efficace des ressources.
5. **Cas d'usage** : <mark style="color:orange;">Les machines virtuelles sont souvent utilisées pour des environnements qui nécessitent une isolation forte ou des systèmes d'exploitation différents</mark>, tandis que <mark style="color:orange;">les conteneurs sont préférés pour les déploiements d'applications légères</mark>, les microservices et les environnements de développement où la rapidité et la portabilité sont cruciales.

## D'un point de vue de l'architecture

Source : [Net Solutions](https://www.netsolutions.com/insights/containerization-vs-virtualization/)

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

Observations:

* L'hyperviseur intègre son propre système d'exploitation alors que le "container engine" partage les propriétés de virtualisation offertes par l'OS (linux).

{% hint style="warning" %}
Avec Docker, sommes-nous en présence d'une architecture qui ressemble plus a un hyperviseur de type I ou II ?
{% endhint %}
