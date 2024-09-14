# Formation devOps

:pill: La capsule

:fire: Documentation d'accompagnement au cycle devOps :fire:

---

## Semaine 1 :computer:

Bases du fonctionnement des outils informatiques - Terminal, scripts, notion de serveur backend

### Jour 1 : Le terminal, Commandes systèmes et pipeline console

---

#### :bike: 1_my_alias

##### Supprimer Blank Space

:point_right:  Récupérez la ressource [myalias.zip](myalias.zip) ci-jointe.

:point_right:  Trouvez une solution afin de supprimer la répétition d’espaces vides dans le fichier "ls.txt" via la commande tr.

:information_source: Utiliser l'option -s pour 'squeeze' (compresser)_

```bash
cat ls.txt| tr -s [:space:]
```

##### Créer un Alias

:point_right:  A partir de la commande alias, créez une nouvelle commande _rm_dbl_space_ dans votre terminal prenant comme paramètre le nom d’un fichier et permettant de supprimer les espaces répétés dans celui-ci.  

_Vous pouvez aller jusqu’à insérer cette instruction dans le fichier ".bashrc" à la racine de votre dossier utilisateur afin de
l’utiliser tout le temps, même après avoir relancé le terminal._

- dans le terminal et/ou dans le fichier ~/.bashrc

```bash
alias rm_dbl_space = "cat $1| tr -s [:space:]"  
```

---

#### :bike: 2_secret_code

---

#### :bike: 3_files_folder

##### Créer et supprimer dossier

:point_right: Récupérez la ressource [filesandfolders.zip](filesandfolders.zip) ci-jointe.

:information_source: Le dossier récupéré qui contient différents fichiers est assez mal rangé, vous allez mieux l’organiser en vous servant uniquement du terminal

```bash
unzip filesandfolders.zip
```

:point_right: Créez un nouveau dossier appelé "txt" dans le dossier "filesandfolders" via la commande mkdir.

```bash
cd filesandfolders
mkdir txt
```

Tout compte fait, ranger ensemble les fichiers de logs dans un dossier "txt" ne semble pas très pertinent…

:point_right: Supprimez le dossier "txt" via la commande rm et créez un répertoire "logs" à la place.

```bash
rm -r txt/
mkdir logs
```

##### Déplacer un fichiers

:point_right: Déplacez le fichier "log1.txt" dans le dossier "logs" via la commande mv.

```bash
mv log1.txt logs/
```

:point_right: Déplacez les fichiers de logs restants dans le dossier "logs" en une seule commande grâce aux wildcards.

```bash
mv log*.txt logs/
```

---

#### :bike: 4_merge_file

##### Fusion de fichiers

:point_right: Récupérez la ressource [mergefiles.zip](mergefiles.zip) ci-jointe.

```bash
unzip mergefiles.zip
```

:point_right: Affichez le contenu du fichier log1.txt via la commande cat.

```bash
cat mergefiles/log1.txt
```

:point_right: Modifiez la commande cat pour afficher le contenu de l’ensemble des fichiers logs présents dans le dossier.

 ```bash
cat mergefiles/log*.txt
```

:point_right: Fusionnez le contenu de tous les fichiers logs du dossier dans un fichier globalLogs.txt en une seule commande.

```bash
cat log*.txt > globalLogs.txt
```

:point_right: Affichez le contenu paginé du fichier globalLogs.txt.

```bash
cat globalLogs.txt | less
```

---

#### :bike: 5_error_logs

##### Filtrer les logs

:point_right: Récupérez la ressource [errorlogs.zip](errorlogs.zip) ci-jointe et unzipez la.

:point_right: Stockez contenu de l’ensemble des fichiers log.txt présents dans le répertoire "errorlogs" dans le fichier globalLogs.txt.

```bash
cat log*.txt > globalLogs.txt
```

:point_right: Filtrez le contenu du fichier globalLogs.txt pour n’afficher que les lignes contenant la mention WARNING.

```bash
grep WARNING globalLogs.txt 
```

:point_right: Stockez le résultat de la commande précédente dans un fichier warningLogs.txt.

```bash
grep WARNING globalLogs.txt > warnings.txt
```

:point_right: Supprimez le fichier globalLogs.txt.

```bash
rm -f globalLogs.txt
```

---

#### :bike: 6_count_lines

##### Compter avec le terminal

:point_right: Récupérez la ressource [countlines.zip](countlines.zip) ci-jointe et unzip-ez la.

:point_right: Affichez le contenu du répertoire via la commande ls.

```bash
ls countlines/
```

 :point_right: Stockez le résultat de la commande précédente dans un fichier "numberLines.txt".

```bash
ls countlines/ > numberLines.txt
```

:point_right: Comptez le nombre de lignes présentes dans le fichier "numberLines.txt".  

_Utiliser la fonction `wc` (pour word count) avec l'option `-l` (pour line)_

```bash
wc -l numberLines.txt
```

---

#### :bike: 7_data_processing

##### Classer par colonne</ins>

:point_right: Récupérez la ressource [dataprocessing.zip](dataprocessing.zip) ci-jointe et unzip-ez la.

:point_right: Trouvez un moyen de trier les données du fichier testLogs.txt par date et stockez le résultat dans un fichier sortedLogs.txt.

:information_source: il faut utiliser l'option -k de sort pour trier par colonne

```bash
sort -k2M -k3n -k4 testLogs.txt > sortedLogs.txt
```

-k2M : Cette option indique à sort de trier en fonction du deuxième champ (colonne) des lignes du fichier, en considérant que ce champ contient des noms de mois (exemple : Jan, Feb, etc.). L'option M fait en sorte que sort interprète ces valeurs comme des mois et les trie dans l'ordre calendaire (Janvier, Février, etc.).

-k3n : Cette option indique à sort de trier ensuite en fonction du troisième champ, en traitant les valeurs de ce champ comme des nombres (n pour numérique). Cela permet un tri numérique correct (exemple : 2 avant 10).

-k4 : Enfin, sort trie en fonction du quatrième champ, en utilisant l'ordre lexicographique (alphabétique par défaut), puisqu'aucune autre option spécifique n'est donnée.

:point_right: Trouvez un moyen d’afficher les colonnes 1 et 6 du fichier sortedLogs.txt et stockez-les dans un fichier data.txt.

:information_source: avec awk (qui considère les espaces et tabulations comme séparateur de colonne par défaut) on lui demande de printer la 1ere et 6e colonne dans le fichier data.txt

```bash
awk '{print $1, $6}' sortedLogs.txt > data.txt
```

---

#### :bike: 8_scores

##### Traitement des données

:point_right: Récupérez la ressource [scores.zip](scores.zip) ci-jointe et unzip-ez la.

:point_right: Trouvez un moyen d’afficher les colonnes 2 et 4 du fichier scores.txt et stockez-les dans un fichier results.txt.

```bash
awk '{print $2, $4}' scores.txt > result.txt
```

:point_right: Trouvez un moyen de calculer la moyenne de toutes les notes présentes dans le fichier results.txt et stockez-la dans un fichier average.txt.

```bash
awk '{sum += $2; count += 1} END {if (count > 0) print "Average =", sum / count}' results.txt > average.txt
```

- sum += $2  
Ajoute la valeur de la deuxième colonne (la note) à la variable sum.  

- count += 1  
Incrémente la variable count pour chaque ligne lue.  

- END {if (count > 0) print "Average =", sum / count}  
À la fin de la lecture du fichier, calcule la moyenne en divisant sum par count et affiche le résultat.

---

#### :bike: 9_find_the_command

##### Manipulation de commandes

:point_right: Trouvez la commande permettant d’afficher le nom de l’utilisateur actif sur la machine et écrivez le résultat de la commande dans le fichier whoami.txt.

```bash
whoami > whoami.txt
```

:point_right: Trouvez la commande permettant de lister l’ensemble des processus en cours et écrivez le résultat de la commande dans le fichier ps.txt.

```bash
ps > ps.txt
```

:point_right: Trouvez la commande permettant d’afficher la valeur d’espace disque disponible sur la machine et écrivez le résultat de la commande dans le fichier df.txt.

:information_source: option -h pour human readable

```bash
df -h
```

:point_right: Trouvez la commande permettant d’afficher les informations du réseau local de la machine et écrivez le résultat de la commande dans le fichier ifconfig.txt.

```bash
ifconfig > ifconfig.txt
```

:point_right: Trouvez la commande permettant de récupérer l’adresse IP publique de la machine via l’URL ifconfig.me et écrivez le résultat de la commande dans le fichier ip.txt.

```bash
curl ifconfig.me > ip.txt
```

---

#### :bike: 10_play_with_pipeline

##### Combinaison de commandes

:point_right: Récupérez la ressource [playwithpipelines.zip](playwithpipelines.zip) ci-jointe

:point_right: Filtrez les lignes du fichier log1.txt contenant le texte INFO via la commande grep.

```bash
cat log1.txt | grep INFO
```

:point_right: Affichez le contenu de tous les fichiers de logs via la commande cat.

```bash
cat log*.txt
```

:point_right: Reprenez les commandes précédentes pour filtrer les lignes INFO sur l’ensemble des fichiers du dossier logs, en une seule commande grâce à une pipeline.

```bash
cat log*.txt | grep INFO
```

---

#### :bike: 11_count_occurences

##### Nombre total d’occurrences

:point_right: Récupérez la ressource [countoccurrences.zip](countoccurrences.zip)

:point_right: En vous servant de la mécanique des pipelines, trouvez une méthode pour compter le nombre d’apparitions du mot INFO dans le fichier log1.txt.

:information_source: l'option -c (count) permet de retourner le total d'apparition du mot cherché

```bash
cat log1.txt | grep -c INFO
```

:point_right: Toujours en vous servant de la mécanique des pipelines, modifiez la commande précédente pour qu’elle retourne le nombre d’apparitions du mot INFO dans l’ensemble des fichiers de logs.

```bash
cat log*.txt | grep -c INFO
```

:point_right: En vous servant de la mécanique des pipelines et de la commande xargs, trouvez le nombre d’apparitions du mot INFO pour chaque fichier.

:information_source: xargs va intervenir sur chaque fichier correspondant au pattern recherché 'log*.txt'

```bash
cat log*.txt | xargs grep -c INFO
```

---

#### :bike: 12_ip_finder

##### Traitement de résultat d’une commande

L’objectif de ce challenge est de construire une commande permettant d’afficher l’IP locale de votre machine à partir du terminal.

:point_right: Exécutez la commande `ip addr show` et observez la réponse obtenue. (exemple de retour console linux ci-dessous)

```bash
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
2: tunl0@NONE: <NOARP> mtu 1480 qdisc noop state DOWN group default qlen 1000
    link/ipip 0.0.0.0 brd 0.0.0.0
4: eth0@if2658: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1440 qdisc noqueue state UP group default 
    link/ether 62:99:26:b1:b8:29 brd ff:ff:ff:ff:ff:ff link-netnsid 0
    inet 192.168.246.109/32 brd 192.168.246.109 scope global eth0
       valid_lft forever preferred_lft forever
```

La réponse est assez longue et contient de nombreuses informations plus ou moins en lien avec ce qui nous intéresse.

:point_right:  Ajoutez en argument le nom de l'interface réseau (dans l'exemple c'est "eth0" mais sur proxmox cela peut ressembler à "enp6s18") à la commande ip addr show et observez la réponse obtenue.

```bash
ip addr show eth0
```

Cette fois-ci la réponse est plus légère et on voit que l’adresse IP que nous recherchons peut être trouvée à la ligne "inet".

```bash
4: eth0@if2658: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1440 qdisc noqueue state UP group default 
    link/ether 62:99:26:b1:b8:29 brd ff:ff:ff:ff:ff:ff link-netnsid 0
    inet 192.168.246.109/32 brd 192.168.246.109 scope global eth0
       valid_lft forever preferred_lft forever
```

:point_right: En complétant la commande précédente et en utilisant la mécanique des pipelines, trouvez une solution pour filtrer la réponse précédente afin qu’elle n’affiche que le contenu de la ligne portant la mention "inet" (et pas "inet6").

```bash
ip addr show eth0 | grep "inet "
```

:point_right: Trouvez une solution pour extraire la deuxième colonne de texte afin de récupérer l’IP au format X.X.X.X/XX et écrire le résultat dans le fichier "ip.txt".

```bash
ip addr show eth0 | grep 'inet ' | awk '{print $2}'
```

- `ip addr show eth0` : Cette commande affiche les informations relatives à l'interface réseau eth0, y compris les adresses IP associées (IPv4 et IPv6), les masques de sous-réseau, et d'autres informations.

- `grep 'inet '` : Cette commande filtre les lignes de la sortie précédente pour ne conserver que celles qui contiennent "inet " (inet espace), qui correspond aux adresses IPv4. Cela élimine les lignes qui n'ont pas d'adresse IPv4 ou qui contiennent d'autres types d'adresses, comme IPv6 (qui est représentée par "inet6").

- `awk '{print $2}'`  : Cette commande extrait la deuxième colonne de la ligne filtrée. Pour la ligne contenant "inet", la deuxième colonne correspond à l'adresse IP suivie du masque de sous-réseau (exemple : 192.168.1.5/24). Le résultat final est donc l'adresse IP et son masque sous forme abrégée.

:cherry_blossom: En résumé, cette commande affiche l'adresse IPv4 (avec son masque de sous-réseau) associée à l'interface réseau demandée - ici "eth0".

---

#### :bike: 13_free_space

##### Traitement du résultat d’une commande

:point_right: L’objectif de ce challenge est de construire une commande permettant d’afficher l’espace libre sur un ou plusieurs disques d’une machine.
Construisez une commande permettant de connaître les informations du disque /dev/sda ou un autre de la machine.

```bash
df -h / | grep -w /dev/sda
```

- df -h / : Cette commande affiche les informations sur l'utilisation du disque pour le système de fichiers qui contient le répertoire racine (/). Le paramètre -h signifie "human-readable"

- grep -w /dev/sda : Cette commande filtre la sortie de df -h pour ne garder que la ligne contenant exactement /dev/sda. L'option -w dans grep assure que le motif recherché (/dev/sda) correspond à un mot entier, évitant ainsi les correspondances partielles avec d'autres noms de périphériques ou chemins.

:cherry_blossom:  En résumé cette commande permet de vérifier l'utilisation du disque du système de fichiers monté sur / (le répertoire racine) et filtre les informations pour ne montrer que celles concernant le périphérique /dev/sda

---

#### :bike: 14_file_sorting

:point_right: Récupérez la ressource [filesorting.zip](filesorting.zip)

:point_right: Construisez une commande permettant de trier les informations du fichier "ls.txt" par poids en bytes.

```bash
cat ls.txt | sort -k 5
```

:point_right: Stockez dans un fichier "largest.txt" les noms des 3 fichiers les plus lourds.

```bash
tr -s '[:space:]' < ls.txt | tr ' ' ':' | sort -t: -k 5 | head -4 > largest.txt
```

---

#### :bike: 15_caesar_cipher

##### Déchiffrement d’un fichier

Le chiffrement de César consiste à substituer une lettre par une autre un plus loin dans l'alphabet, c'est-à-dire qu'une lettre est toujours remplacée par la même lettre et que l'on applique le même décalage à toutes les lettres, cela rend très simple le décodage d'un message puisqu'il n’y a que 25 décalages possibles.
Exemple : ABC avec un décalage de 1 vers la droite donne BCD.

:point_right: Récupérez la ressource [caesarcipher.zip](caesarcipher.zip)

:point_right: Trouvez une méthode pour déchiffrer le contenu du fichier cipher.txt et stockez-le dans le fichier message.txt.

_Note : le décalage est de 3 lettres, à vous de déterminer si le décalage est vers la droite (A -> D) ou vers la gauche (X <- A)._

```bash
cat cipher.txt | tr "[X-ZA-W]" "[A-Z]" > caesar.txt
```
