
La première chose à faire est de mettre à jour les paquets existants sur votre VPS. 
Cela garantit que vous disposez des dernières mises à jour de sécurité et des améliorations logicielles.


## Mise à Jour du Système 
```bash
apt update && apt upgrade -y
```

## Installation des Paquets Essentiels 
```bash
apt install -y sudo wget git vim apt-transport-https ca-certificates curl gnupg net-tools jq
apt autoremove -y
```
Voici une brève description de chacun de ces paquets :

- `sudo` : Permet à un utilisateur d'exécuter des commandes en tant qu'un autre utilisateur, souvent l'utilisateur root.
- `wget` : Utilitaire de téléchargement de fichiers depuis le web.
- `git` : Système de contrôle de version distribué pour gérer le code source.
- `vim` : Éditeur de texte avancé pour modifier des fichiers de configuration et du code.
- `apt-transport-https` : Permet à apt de récupérer des paquets via HTTPS.
- `ca-certificates` : Paquets de certificats racine pour vérifier les certificats SSL.
- `curl` : Outil de ligne de commande pour transférer des données avec des URL.
- `gnupg` : Outil pour la gestion des clés et la sécurité des communications.
- `net-tools` : Suite d'outils réseau comme ifconfig et netstat.
- `jq` : Utilitaire de manipulation de données JSON.

Ces étapes de mise à jour et d'installation des paquets sont essentielles pour assurer la sécurité et la fonctionnalité de votre VPS. En suivant ces commandes, vous préparez votre serveur pour les prochaines étapes de configuration et de déploiement.
