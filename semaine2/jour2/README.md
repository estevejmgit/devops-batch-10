# Formation devOps

:pill: La capsule

:fire: Exercices et corrections formation devOps :fire:

---

## Semaine 2 - BDD, Réseaux, SSH, GIT

### Jour 2 : Les équipements réseau - GNS3

---

#### :warning: de manière globale 

Plusieurs exercices importés avec CISCO ne marchent pas comme attendu (ex awesomelab)

_solution de contournement : installer openWRT et configurer comme préconisé ci-dessous_

De manière générale toujours, il arrive que les debian-server n’arrivent pas à récupérer d’addresse ip avec dhcp :

```bash
sudo nano /etc/network/interfaces
```
décommenter les 2 lignes sous DHCP :

```bash
ens4
iface ens4 inet dhcp
```

puis

```bash
sudo /etc/init.d/networking restart
```

#### :information_source: CHALLENGE DEBIAN IN THE LAN

La ressource n’est pas dispo sur Ariane. > [Lien pour la télécharger](https://static.lacapsule.academy/programs/devops-full-time/J10/debianinthelan.zip) <
_ne pas oublier de supprimer le routeur CISCO et le remplacer par openWRT_

---

#### :bike: Création d’un réseau avec routeur

- Installer OpenWRT (1er à apparaître dans la liste des devices) et pas Cisco
(la video devient obsolète)
- Remplacer “Internet” par un élément “Cloud”, configurer cet élément Cloud sur eth0
- Connecter openWRT (eth1) vers Cloud (eth0)

#### :bike: Setup du service DHCP sur le routeur openWRT

```bash
uci -q delete dhcp.@dnsmasq[0].server 
uci add_list dhcp.@dnsmasq[0].server="8.8.8.8" 
uci add_list dhcp.@dnsmasq[0].server="8.8.4.4" 
uci commit dhcp 
service dnsmasq restart
```

#### :bike: Sur les VM PC pour récupérer une ip

```bash
ip dhcp
```

#### :bike: Sur les machines Debian pour récupérer une ip

```bash
sudo /etc/init.d/networking restart
```

Sur les machine Debian il est peut-être nécessaire de changer le fichier /etc/network/interfaces

```bash
sudo nano /etc/network/interfaces
```

Sous la ligne #DHCP, décommenter les deux lignes suivantes :

```bash
auto ens4
iface ens4 inet dhcp
```

Redémarrer networking

```bash
sudo /etc/init.d/networking restart
```
