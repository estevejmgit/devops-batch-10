 # Formation devOps
_La capsule_

:fire: Exercices et corrections formation devOps :fire:

---
## Semaine 1 :computer: 

Bases du fonctionnement des outils informatiques - Terminal, scripts, notion de serveur backend 

### Jour 1 : Le terminal, Commandes systèmes et pipeline console

---

#### :bike: 1_my_alias

##### <ins> Supprimer Blank Space </ins>

👉 Récupérez la ressource "myalias.zip" ci-jointe.

👉 Trouvez une solution afin de supprimer la répétition d’espaces vides dans le fichier "ls.txt" via la commande tr.

_Utiliser l'option -s_

```
cat ls.txt| tr -s [:space:]
```

##### <ins> Créer un Alias </ins>

👉 A partir de la commande alias, créez une nouvelle commande delspace dans votre terminal prenant comme paramètre le nom d’un fichier 
et permettant de supprimer les espaces répétés dans celui-ci.
_Vous pouvez aller jusqu’à insérer cette instruction dans le fichier ".bashrc" à la racine de votre dossier utilisateur afin de
l’utiliser tout le temps, même après avoir relancé le terminal._

- dans le terminal et/ou dans ~/.bashrc

```
alias rm_dbl_space = "cat $1| tr -s [:space:]"  
```

---

#### :bike: 2_secret_code

---

#### :bike: 3_files_folder

##### <ins> Créer et supprimer dossier </ins>

:point_right: Récupérez la ressource [filesandfolders.zip](filesandfolders.zip) ci-jointe.

_Le dossier récupéré qui contient différents fichiers est assez mal rangé, vous allez mieux l’organiser en vous servant uniquement du terminal_

```
unzip filesandfolders.zip
```

:point_right: Créez un nouveau dossier appelé "txt" dans le dossier "filesandfolders" via la commande mkdir.

```
cd filesandfolders
mkdir txt
```

Tout compte fait, ranger ensemble les fichiers de logs dans un dossier "txt" ne semble pas très pertinent…

:point_right: Supprimez le dossier "txt" via la commande rm et créez un répertoire "logs" à la place.

```
rm -r txt/
mkdir logs
```

##### <ins> Déplacer un fichiers </ins>

:point_right: Déplacez le fichier "log1.txt" dans le dossier "logs" via la commande mv.

```
mv log1.txt logs/
```

:point_right: Déplacez les fichiers de logs restants dans le dossier "logs" en une seule commande grâce aux wildcards.

```
mv log*.txt logs/
```

---

#### :bike: 4_merge_file

##### <ins> Fusion de fichiers </ins>

:point_right: Récupérez la ressource [mergefiles.zip](mergefiles.zip) ci-jointe.

```
unzip mergefiles.zip
``` 

:point_right: Affichez le contenu du fichier log1.txt via la commande cat.

```
cat mergefiles/log1.txt
```

:point_right: Modifiez la commande cat pour afficher le contenu de l’ensemble des fichiers logs présents dans le dossier.

 ```
cat mergefiles/log*.txt
```

:point_right: Fusionnez le contenu de tous les fichiers logs du dossier dans un fichier globalLogs.txt en une seule commande. 

```
cat log*.txt > globalLogs.txt
```

:point_right: Affichez le contenu paginé du fichier globalLogs.txt.

```
cat globalLogs.txt | less
```

---

#### :bike: 5_error_logs

##### <ins> Filtrer les logs </ins>

:point_right: Récupérez la ressource [errorlogs.zip](errorlogs.zip) ci-jointe et unzipez la.

:point_right: Stockez contenu de l’ensemble des fichiers log.txt présents dans le répertoire "errorlogs" dans le fichier globalLogs.txt.

```
cat log*.txt > globalLogs.txt
```

:point_right: Filtrez le contenu du fichier globalLogs.txt pour n’afficher que les lignes contenant la mention WARNING.

```
grep WARNING globalLogs.txt 
```

:point_right: Stockez le résultat de la commande précédente dans un fichier warningLogs.txt.


```
grep WARNING globalLogs.txt > warnings.txt
```

:point_right: Supprimez le fichier globalLogs.txt.


```
rm -f globalLogs.txt
```
---

#### :bike: 6_count_lines


##### <ins> Compter avec le terminal </ins>


:point_right: Récupérez la ressource "countlines.zip" ci-jointe et unzip-ez la.

:point_right: Affichez le contenu du répertoire via la commande ls.

```
ls countlines/
```

 :point_right: Stockez le résultat de la commande précédente dans un fichier "numberLines.txt". 

 
```
ls countlines/ > numberLines.txt
```

:point_right: Comptez le nombre de lignes présentes dans le fichier "numberLines.txt".  
_Utiliser la fonction `wc` (pour word count) avec l'option `-l` (pour line)_

```
wc -l numberLines.txt
```
---

#### :bike: 7_data_processing

##### <ins> Classer par colonne</ins>


:point_right: Récupérez la ressource "dataprocessing.zip" ci-jointe et unzip-ez la.

:point_right: Trouvez un moyen de trier les données du fichier testLogs.txt par date et stockez le résultat dans un fichier sortedLogs.txt.

_il faut utiliser l'option -k de sort pour trier par colonne_

```
sort -k2M -k3n -k4 testLogs.txt > sortedLogs.txt
```

:point_right: Trouvez un moyen d’afficher les colonnes 1 et 6 du fichier sortedLogs.txt et stockez-les dans un fichier data.txt.

_avec awk (qui considère les espaces et tabulations comme séparateur de colonne par défaut) on lui demande de printer la 1ere et 6e colonne dans le fichier data.txt_

```
awk '{print $1, $6}' sortedLogs.txt > data.txt
```
----

#### :bike: 8_scores

##### <ins> Traitement des données </ins>

:point_right: Récupérez la ressource [scores.zip](scores.zip) ci-jointe et unzip-ez la.

:point_right: Trouvez un moyen d’afficher les colonnes 2 et 4 du fichier scores.txt et stockez-les dans un fichier results.txt.

```
awk '{print $2, $4}' scores.txt > result.txt
```

:point_right: Trouvez un moyen de calculer la moyenne de toutes les notes présentes dans le fichier results.txt et stockez-la dans un fichier average.txt.

```
awk '{sum += $2; count += 1} END {if (count > 0) print "Average =", sum / count}' results.txt > average.txt
```

> [!INFO]
> sum += $2 : Ajoute la valeur de la deuxième colonne (la note) à la variable sum.  
> count += 1 : Incrémente la variable count pour chaque ligne lue.  
> END {if (count > 0) print "Average =", sum / count} : À la fin de la lecture du fichier, calcule la moyenne en divisant sum par count et affiche le résultat. 

----

#### :bike: 9_find_the_command

##### <ins> Manipulation de commandes </ins>

:point_right: Trouvez la commande permettant d’afficher le nom de l’utilisateur actif sur la machine et écrivez le résultat de la commande dans le fichier whoami.txt.

```
whoami > whoami.txt
```
:point_right: Trouvez la commande permettant de lister l’ensemble des processus en cours et écrivez le résultat de la commande dans le fichier ps.txt.

```
ps > ps.txt
```

:point_right: Trouvez la commande permettant d’afficher la valeur d’espace disque disponible sur la machine et écrivez le résultat de la commande dans le fichier df.txt.

_option -h pour human readable_

```
df -h
```

:point_right: Trouvez la commande permettant d’afficher les informations du réseau local de la machine et écrivez le résultat de la commande dans le fichier ifconfig.txt.

```
ifconfig > ifconfig.txt
```

:point_right: Trouvez la commande permettant de récupérer l’adresse IP publique de la machine via l’URL ifconfig.me et écrivez le résultat de la commande dans le fichier ip.txt.

```
curl ifconfig.me > ip.txt
```

---

#### :bike: 10_play_with_pipeline

---

#### :bike: 11_count_occurences

---

#### :bike: 12_ip_finder

---

#### :bike: 13_free_space

---

#### :bike: 14_file_sorting

---

#### :bike: 15_caesar_cipher
