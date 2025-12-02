# Gestion d'images

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

