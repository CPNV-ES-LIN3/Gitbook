# Evaluation NTP Pratique

## Critères globaux

| Critère             | Description                                                                                                                                                  |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Forme collaborative | Par équipe de 3 techs                                                                                                                                        |
| Moyens              | <ul><li>Votre dépôt github (code + documentation)</li><li>Un accès à l'infrastructure de <em>staging</em> via un terminal</li><li>Papier et crayon</li></ul> |
| Temps à diposition  | 3 périodes                                                                                                                                                   |
| Pondération         | 50% de la note NTP                                                                                                                                           |

## Grille d'évaluation

Le respect des consignes est crucial. L'épreuve peut être annulée si une équipe ne se conforme pas aux consignes.

| Elément      | Valeur |
| ------------ | ------ |
| SRV NTP (DC) | 50%    |
| CLIENTS      | 25%    |
| FAILOVER     | 25%    |

## Partie I - Déploiement du protocole NTP

### Contexte

Chaque équipe reçoit une infrastructure de _staging_ identique à celle utilisée la semaine précédente. Les instances ont été réinitialisées. Tous les paramètres vous permettant de vous y connecter, <mark style="color:$danger;">à l'exception des mots de passe Windows</mark>, sont restés inchangés.

{% hint style="info" %}
Le fichier partagé via OneDrive vous permettra de récupérer le nouveau mot de passe !
{% endhint %}

Les paramètres du réseau tels que la sécurité, les types d'OS, les architectures des machines sont également identiques.

### Étape 01 - Validation de l'infrastructure

Cette étape est dédiée à la prise en main de l'infrastructure et à la vérification que tout ce dont vous avez besoin est disponible, **avant de déployer NTP**.

{% hint style="danger" %}
**LIVRABLE I**\
Vous mentionnez à votre enseignant, via le canal Teams ouvert pour l'évaluation, que tout est en ordre et que vous débutez la configuration du NTP.\
\
Sinon, vous demandez qu'un correctif soit apporté à l'infrastructure.
{% endhint %}

### Étape 02 - Configuration du protocole NTP

En utilisant uniquement le contenu de votre dépôt GitHub, mettez en place le protocole NTP **sans réaliser les scénarios décrits dans le backlog**.

{% embed url="https://github.com/orgs/CPNV-ES-LIN3/projects/9" %}

{% hint style="danger" %}
**LIVRABLE II**

Vous mentionnez à votre enseignant, via le canal Teams ouvert pour l'évaluation, que le déploiement est terminé et que vous êtes prêts à faire la démonstration.\
\
Vous arrêtez les trois instances.
{% endhint %}

L'enseignant relancera les instances une fois que toutes les équipes seront prêtes.

### Étape 03 - Préparation du backlog

Avant de débuter la démonstration, il est important de mettre à jour votre Backlog sur GitHub Project.\
\
**TODO** : si vous n'avez pas du tout traiter l'issue

**IN PROGRESS** : issue non terminée (à discuter)

**IN REVIEW** : prêt à être démontré

**DONE** : uniquement si la validation de l'enseignant a été obtenue

{% hint style="danger" %}
**LIVRABLE III**\
Dès que le backlog est à jour, mentionnez-le via Teams en postant le lien de votre projet Github Projects.
{% endhint %}

### Étape 04 - Démonstration et preuves techniques

Cette étape est la plus importante. Elle doit valider que votre implémentation est fonctionnelle et que vous maîtrisez la solution livrée.

Vous recevrez des consignes étape par étape, à suivre précisément.

{% hint style="warning" %}
Note : il ne s'agit pas d'un cours, mais d'une évaluation.\
\
Le dialogue est attendu lors du Pôle 1, uniquement.
{% endhint %}
