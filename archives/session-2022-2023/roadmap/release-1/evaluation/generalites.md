# Généralités

### Données sensibles

* Se questionner sur le niveau de confidentialité de la documentation :
  * Adresses ip privées.
  * Nom d'utilisateur.
  * Mot de passe.

### Justifier les choix technologiques

* [Choix entre NTP et Chrony](https://chrony.tuxfamily.org/comparison.html) ?

### Prouver

* Chaque commande doit être accompagnée de la méthode pour valider que le résultat obtenu est le bon.
* Le service qui est mis en place doit être testé (analyse des stratums).

### Problèmes présents

* Les problèmes non résolus doivent être documentés.

### Pré-requis

* Bien séparer les pré-requis de la procédure d'installation
  * fail2ban dans ntp.
  * purge ntp.
  * DNS avant la configuration de Kerberos.

### Expliquer les commandes

* En lisant la commande, on doit pouvoir comprendre ce que vous faites.
  * sudo timedatectl set-ntp true.

### Configuration de base

* Sauvegarder les fichiers de conf avant de les modifier.
* Les nettoyer
  * Real Kerberos MIT.
  * NTP sécurisé (clés asymétriques).

### Utilisation de logs

* Les activer pour valider que l'installation se comporte correctement.
* Mettre en place une rotation (sur apache on attend très rapidement 1Go de log).

### Sources

* Attention au plan légal.
* Mentionnez les sources à l'endroit où elles ont été utiles afin d'appuyer votre documentation.
* Vos collègues sont aussi des sources.
