Pour sécuriser et administrer efficacement notre VPS, il est essentiel de gérer correctement les utilisateurs et de configurer SSH (Secure Shell). Cette section décrit les étapes nécessaires pour ajouter un nouvel utilisateur avec des privilèges sudo et pour configurer SSH afin d'améliorer la sécurité.

## Ajout d'un Nouvel Utilisateur

La première étape consiste à ajouter un nouvel utilisateur qui sera utilisé pour les connexions et les tâches administratives.

### Commandes pour Ajouter un Utilisateur

Exécutez les commandes suivantes pour créer un nouvel utilisateur nommé `jeremi` pour l'exemple et avec les privilèges nécessaires :

```bash
# Ajouter un nouvel utilisateur avec un home directory, un user ID spécifique, et des groupes users et sudo
useradd -m -u 1001 -G users,sudo -s /bin/bash jeremi

# Définir un mot de passe pour le nouvel utilisateur
passwd jeremi

# Ajouter une entrée dans sudoers pour permettre à l'utilisateur jeremi d'exécuter des commandes sudo sans mot de passe
echo "jeremi ALL=(ALL) NOPASSWD:ALL" | tee /etc/sudoers.d/jeremi
```

## Configuration de SSH

Pour améliorer la sécurité de notre serveur, nous allons configurer SSH pour désactiver les connexions root et restreindre l'accès SSH à notre nouvel utilisateur.

### Commandes pour Configurer SSH

Exécutez les commandes suivantes pour modifier la configuration SSH :

```bash
# Désactiver les connexions SSH root
sed -i -r "s/PermitRootLogin .*/PermitRootLogin no/g" /etc/ssh/sshd_config
grep PermitRootLogin /etc/ssh/sshd_config

# Ajouter une règle pour autoriser uniquement l'utilisateur jeremi à se connecter via SSH
echo 'AllowUsers jeremi' | sudo tee -a /etc/ssh/sshd_config

# N'oubliez pas de redémarrer le service SSH pour appliquer les modifications :
systemctl restart ssh
```

## (Optionnel) Changement du Port SSH

Pour une sécurité supplémentaire, vous pouvez changer le port par défaut utilisé par SSH. Décommentez et modifiez la ligne suivante dans /etc/ssh/sshd_config :

```bash
# Modification du port 22 par 1221
sed -i -r "s/#Port 22/Port 1221/g" /etc/ssh/sshd_config

# Gestion d'une regele iptables pour autoriser les connexions sur le nouveau port :
iptables -A INPUT -m state --state NEW -m tcp -p tcp --dport 1221 -j ACCEPT
```

## Conclusion

En suivant ces étapes, vous configurez un environnement utilisateur sécurisé et optimisé pour l'administration de votre VPS. La gestion appropriée des utilisateurs et la configuration de SSH sont des éléments clés pour maintenir la sécurité et l'intégrité de votre serveur.

