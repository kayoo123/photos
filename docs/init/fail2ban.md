Fail2Ban est un logiciel de sécurité qui protège votre serveur en surveillant les journaux de services pour détecter les tentatives de connexion échouées et en bloquant les adresses IP qui les effectuent. Cela permet de prévenir les attaques par force brute et d'autres menaces similaires.

## Installation de Fail2Ban

La première étape consiste à installer Fail2Ban ainsi qu'iptables, qui sera utilisé pour appliquer les règles de blocage.

Exécutez les commandes suivantes pour mettre à jour votre système et installer Fail2Ban et iptables :

```bash
apt update && apt install -y fail2ban iptables
```

## Configuration de Fail2Ban

Pour que Fail2Ban puisse surveiller les journaux de connexion SSH votre serveur, nous devons créer les répertoires et fichiers nécessaires. Dans cet exemple, nous configurons également Fail2Ban pour surveiller les journaux de Traefik (proxy-web).

```bash
mkdir /var/log/traefik/
touch /var/log/traefik/access.log
```

Nous allons maintenant créer deux fichiers de configuration personnalisé pour Fail2Ban: 

#### `custom.conf` : Gere le comportement du service fail2ban

```bash
cat <<EOF > /etc/fail2ban/jail.d/custom.conf
[DEFAULT]
ignoreip = 127.0.0.1 $(hostname -I)
findtime = 20m
bantime = 24h
maxretry = 2

[sshd]
backend = systemd
EOF
```

- `ignoreip` : Adresses IP à ignorer par Fail2Ban (ajoutez l'adresse IP de votre serveur).
- `findtime` : Période de recherche des tentatives de connexion échouées.
- `bantime` : Durée du bannissement des IP en cas de tentatives échouées répétées.
- `maxretry` : Nombre maximum de tentatives échouées avant de bannir une IP.


#### `traefik.conf` : Gestion des connexions basic-auth sur vos services

```bash
cat <<EOF > /etc/fail2ban/jail.d/traefik.conf
[traefik-auth]
enabled = true
chain = DOCKER-USER
logpath = /var/log/traefik/access.log
port = http,https
EOF
```

- `enabled` : Active la surveillance de Traefik.
- `chain` : Chaîne iptables où les règles de blocage seront appliquées.
- `logpath` : Chemin vers le fichier de journalisation de Traefik.
- `port` : Ports à surveiller (HTTP et HTTPS).

## Activation et Redémarrage de Fail2Ban

Pour appliquer les nouvelles configurations, redémarrez le service Fail2Ban et configurez-le pour qu'il se lance automatiquement au démarrage du serveur :

```bash
systemctl restart fail2ban
systemctl enable fail2ban
fail2ban-client status
```

## Conclusion

L'installation et la configuration de Fail2Ban ajoutent une couche de sécurité essentielle à votre serveur en bloquant les adresses IP malveillantes. En suivant ces étapes, vous protégez efficacement votre VPS contre les attaques par force brute et autres tentatives de connexion non autorisées.
