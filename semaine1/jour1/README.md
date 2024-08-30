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


:point_right: Récupérez la ressource "errorlogs.zip" ci-jointe et unzip-ez la.

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

---

#### :bike: 7_data_processing

----

#### :bike: 8_scores

----

#### :bike: 9_find_the_command

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
