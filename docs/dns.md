# Qu'est-ce qu'un DNS ?

DNS signifie **Domain Name System** (système de noms de domaine). 

C'est un système qui traduit les noms de domaine lisibles par l'homme (comme `www.exemple.com`) en adresses IP que les ordinateurs utilisent pour identifier les ressources sur le réseau (comme `192.168.1.1`). 

En d'autres termes, le DNS agit comme un annuaire téléphonique pour Internet, permettant aux utilisateurs de se connecter aux sites Web en utilisant des noms de domaine faciles à retenir plutôt que des adresses IP numériques.

## Qu'est-ce que freeDNS ?

**[freeDNS](https://freedns.afraid.org/)** est un service de DNS gratuit qui permet aux utilisateurs de gérer leurs propres enregistrements DNS sans frais. 

## Exemple pour mon domaine : **photos.jeremi.fr.to**

Apres avoir validé mon inscription et m'y etre connecté, il suffit de se rendre sur : 

- l'onglet: `Subdomains`
- de cliquer sur `Add a new subdomain`, et de renseigner 
  - type : `A`
  - subdomain : `photos.jeremi`
  - domain: `fr.to (public)` (a chercher en cliquant sur 'many many more available > [Shared Domain Registry](https://freedns.afraid.org/domain/registry/)')
  - destination: `45.149.206.155` (renseigner l'ip de votre machine virtuel)
  - renseigner le captcha et valider avec `save`.

Il nous reste a valider que la resolution fonctionne bien depuis n'importe quel ordinateur : 

```bash
host photos.jeremi.fr.to
photos.jeremi.fr.to has address 45.149.206.155
```

Parfait :)
A présent, tous les ordinateurs du monde arrive à ...

En utilisant un service freeDNS, vous bénéficierez d'une gestion DNS efficace sans les coûts associés a ce type de services.


