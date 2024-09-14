# Formation devOps

:pill: La capsule

:fire:  Documentation d'accompagnement au cycle devOps :fire:

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
:accessibility: La commande dig devrait retourner des infos dans lesquelles on va retrouver l’IP de votre debian-DNS


#### :bike: Configuration du serveur DNS

:point_right: Grâce à bind9, faîtes en sorte que le site hébergé sur le serveur web puisse être joignable par d’autres machines depuis le nom de domaine "awesome.lab".

- Configurer bind9 pour le domaine awesome.lab

```bash
sudo nano /etc/bind/named.conf.local
```

- Ajouter ce bloc de code dans le fichier `named.conf.local`

```bash
zone "awesome.lab" {
	type master;
	file "/etc/bind/db.awesome.lab";
};
```

- Créer et modifier un fichier de zone `db.awesome.lab` à partir du template déjà présent

```bash
sudo cp /etc/bind/db.local /etc/bind/db.awesome.lab
sudo nano  /etc/bind/db.awesome.lab
```

- Modifier les entrées pour qu'elles correspondent au domaine awesome.lab et à l'adresse IP du serveur Apache.

```bash
$TTL	604800
@   	IN  	SOA 	ns.awesome.lab. root.awesome.lab. (
                      	2     	; Serial
                 	604800     	; Refresh
                  	86400     	; Retry
                	2419200     	; Expire
                 	604800 )   	; Negative Cache TTL
;

@   	IN  	NS  	ns.awesome.lab.
ns  	IN  	A   	192.168.1.10  ; Adresse IP de ton serveur DNS (machine BIND9)
@   	IN  	A   	192.168.1.20  ; Adresse IP de ton serveur Apache
www 	IN  	A   	192.168.1.20  ; Alias pour le serveur Apache
```

- Vérifier la syntaxe du fichier créé

```bash
sudo named-checkzone awesome.lab /etc/bind/db.awesome.lab
```

- Restart de bind9 pour prendre en compte le changement

```bash
sudo systemctl restart bind9
```

#### :bike: Configuration du serveur APACHE pour awesome.lab

- Création d’un virtual-host pour awesome.lab

```bash
sudo nano /etc/apache2/sites-available/awesome.lab.conf
```

- Contenu du fichier de conf

```bash
<VirtualHost *:80>
	ServerName awesome.lab
	ServerAlias www.awesome.lab
	DocumentRoot /var/www/awesome.lab

	<Directory /var/www/awesome.lab>
    	Options Indexes FollowSymLinks
    	AllowOverride All
    	Require all granted
	</Directory>

	ErrorLog ${APACHE_LOG_DIR}/awesome.lab_error.log
	CustomLog ${APACHE_LOG_DIR}/awesome.lab_access.log combined
</VirtualHost>
```

- Création d’un répertoire et d’un fichier index.html pour le site awesome.lab

```bash
sudo mkdir /var/www/awesome.lab
echo "<h1>Welcome to awesome.lab!</h1>" | sudo tee /var/www/awesome.lab/index.html
```

- Activation du site awesome.lab et relaod de Apache

```bash
sudo a2ensite awesome.lab.conf
sudo systemctl reload apache2
```

#### :bike: Vérification de la config

- Depuis la VM CLiente on doit pouvoir accéder en http au site awesome.lab

```bash
curl http://awesome.lab
```

> Renvoie le code HTML brut de la page index.html

```bash
dig awesome.lab
```

> Renvoie les informations détaillées des DNS utilisées 


