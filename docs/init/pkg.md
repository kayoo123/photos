Une fois la premiere connexion bien établie sur notre VPS, nous allons immediatement procéder a sa mise-a-jour ainsi qu'a l'installation de paquage.
Ces étapes étant relativement simple, je ne rentrerai pas dans le détail.

## update 
```bash
apt update && apt upgrade -y
```

## Paquages 
```bash
apt install -y sudo wget git vim apt-transport-https ca-certificates curl gnupg net-tools jq
apt autoremove -y
```
