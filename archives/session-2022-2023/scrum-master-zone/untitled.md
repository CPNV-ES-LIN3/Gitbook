---
description: >-
  Cette page synthétise le retour d'expérience du Scrum Master sur le projet
  LIN3
---

# Suivi des équipes

### NGY - le 27-nov-2020 - Feedback NTP

La prise en main du NTP client semble être aisée, y compris lorsque les concepts du NTP ne sont pas acquis. Ceci ne permet malheureusement "que" de le faire tourner. On est au niveau utilisateur d'un service. Difficile à ce stade de valider que tout fonctionne bien. "Ca semble marcher".

Lorsque qu'ils doivent mettre en place leur propre serveur source vient le questionnement sur l'intérêt du NTP et de la synchronisation d'horloge.

Les documentations Microsoft ont tendances à pousser pour l'utilisation d'un AD (qui s'en charge lors de l'intégration du client dans le domaine).

A la question, "est-ce que le NTP se protège ?". Peu apercoive la mention de Dos (intervalle de demande synchronisation < 4 secondes tout comme l'utilisation du ibust). Attention à bien en parler avec eux.

Le schéma de l'infra ne semble pas leur être important. La notion d'architecture du NTP n'est pas évidente. Client Server ok. Mais la communication horizontale tout comme le peer-to-peer doivent être discutés avec eux.





