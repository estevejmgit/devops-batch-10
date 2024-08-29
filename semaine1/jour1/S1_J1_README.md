 # Formation devOps
_La capsule_

:fire: Exercices et corrections formation devOps :fire:

---
## Semaine 1 :computer: 

Bases du fonctionnement des outils informatiques - Terminal, scripts, notion de serveur backend 

### Jour 1 : Le terminal, Commandes systèmes et pipeline console

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

#### :bike: 2_secret_code

#### :bike: 3_files_folder

#### :bike: 4_merge_file

#### :bike: 5_error_logs

#### :bike: 6_count_lines

#### :bike: 7_data_processing

#### :bike: 8_scores

#### :bike: 9_find_the_command

#### :bike: 10_play_with_pipeline

#### :bike: 11_count_occurences

#### :bike: 12_ip_finder

#### :bike: 13_free_space

#### :bike: 14_file_sorting

#### :bike: 15_caesar_cipher
