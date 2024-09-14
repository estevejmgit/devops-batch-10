# Formation devOps

:pill: La capsule

:fire: Exercices et corrections formation devOps :fire:

---

## Semaine 2 - BDD, Réseaux, SSH, GIT

### Jour 3 : Adresse iP, ports et protocoles - GNS3

---

#### :warning: de manière globale 

Plusieurs exercices importés avec CISCO ne marchent pas comme attendu 

De manière générale toujours, il arrive que les debian-server n’arrivent pas à récupérer d’addresse ip avec dhcp :

> config réseau openWRT comme pour le [jour2](jour2/)
> 

:information_source: NMAP une fois lancé ne fait de retour que quand le scan est fini, et selon la taille des infos demandées/le nombre d'équipements connectés, cela peut prendre quelques minutes avec un PC puissant, et encore plus avec une VM dans une VM. Soyez patient, le résultat viendra toujours

---

#### :bike: Challenge FTP :

Sur debian -server si il n’y a que openssh-sftpserver d’installé et pas de user “lacapsule”

:point_right: se connecter avec debian/debian en sftp direct depuis le client, 
ou installer vsftpd sur le server pour se connecter depuis la CLI ftp du Client.

_Dans tous les cas on peut créer un user “lacapsule” mdp “lacaspule” s i on veut éviter d’utiliser debian sur le server_


#### :bike: HACKATHON AWESOMELAB

##### :eagle: Pré-requis

- Un routeur openWRT connecté à internet avec un DHCP activé
- Une Debian 12 avec Bind9 installé pour les DNS qui récupère son IP en DHCP
- Une Debian 12 avec Apache2 installé, qui récupère son IP en DHCP
- Une VM Cliente qui récupère son IP en DHCP

:point_right: Assurez-vous que toutes les requêtes DNS passent par votre propre serveur DNS plutôt que par celui configuré par défaut sur le routeur.

- Récupérer l’IP de la Debian-DNS

```bash
ip a show
```

- Sur Debian-Apache et VM Cliente, changer /etc/resolv.conf pour y mettre l’IP du DNS

```bash
sudo nano /etc/resolv.conf
```

- sur la ligne nameserver mettre l’IP du DNS

```bash
nameserver IP_DEBIAN_DNS
```

- Vérifier la prise en compte de ce changement avec la commande dig de la lib  dnsutils

```bash
sudo apt update
sudo apt install dnsutils
dig google.com
```

