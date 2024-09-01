# Formation devOps

:pill: La Capsule

:fire: Exercices et corrections formation devOps :fire:

---

## Semaine 1 :computer:

Bases du fonctionnement des outils informatiques - Terminal, scripts, notion de serveur backend

### Jour 2 : Scripting & Droits Linux

---

#### :bike: 1_Execute my script

##### Création d’un premier script

Vous utiliserez l’utilitaire nano pour créer vos scripts afin de bénéficier d’un éditeur de texte intégré au terminal.
Pour créer et éditer un nouveau fichier, il suffit d’utiliser la commande suivante : nano nomDuFichier.extension.

:point_right:  Exécutez la commande `nano myscript.sh` et copiez le code suivant dans la fenêtre de l’éditeur de texte :

```bash
#!/usr/bin/env bash

echo "Hello world!"
```

:keyboard: Sauvegardez le fichier en appuyant sur les touches `CTRL + X`, puis en appuyant sur `y` (yes) et enfin sur `Enter`.

##### Exécution d’un script

Votre script a bien été créé et vous allez maintenant l’exécuter à l’aide de votre terminal.

Pour cela, la première chose à faire est de donner les droits d’exécution au script.

:point_right: Exécutez la commande suivante.

```bash
chmod +x myscript.sh
```

:keyboard: Sauvegardez le fichier en appuyant sur les touches `CTRL + X`, puis en appuyant sur `y` (yes) et enfin sur `Enter`.

Pour rappel, la commande chmod (abréviation de "change mode") permet de changer les permissions d’un fichier donné. La mention +x indique que nous souhaitons rendre ce fichier exécutable.

:point_right: Exécutez le script contenu dans le fichier myscript.sh avec la commande suivante.

```bash
./myscript.sh
```

---

#### :bike: 2_Echo echo

##### Variables simples

Le script du challenge précédent était relativement simple et ne servait qu’à afficher la chaîne de caractères "Hello world". C’est un bon début, mais il est possible d’aller plus loin dans la commande echo.

:point_right: À l’aide de nano, créez un nouveau fichier appelé variables.sh contenant le code suivant.

```bash
#!/usr/bin/env bash

firstname=john
echo "home folder /home/$firstname" 
```
:point_right: Rendez le fichier exécutable.

```bash
chmod +x myscript.sh
```

:point_right: Exécutez le script.

```bash
./myscript.sh
```

_Vous avez stocké la chaîne de caractères "john" dans la variable "firstname", ainsi la chaîne de caractères affichée dans le terminal correspond à "home folder /home/john"._

:point_right: Remplacez le contenu de la variable "firstname" par "vanessa" et exécutez à nouveau le script :  

_la chaîne de caractères affichée dans le terminal correspond à "home folder /home/vanessa"._

##### Variables d’environnement

Les variables permettent de stocker des valeurs et de les réutiliser ou de les mettre à jour en y faisant appel.

Il existe également des variables définies de manière globale au sein de votre terminal, on les appelle variables d’environnement et celles-ci contiennent des informations utiles pouvant être transmises aux processus de votre session shell.

:point_right: Depuis votre terminal, exécutez la commande `printenv HOME`.

_Cette commande retourne le chemin d’accès vers le répertoire par défaut de votre terminal qui devrait ressembler à ça :_

```bash
/home/engineer
```

:blossom: Affichez la liste de toutes les variables d’environnement avec la commande `printenv`.

##### Variables prépositionnées

Il est possible de transmettre des valeurs à stocker dans des variables via les paramètres du script, il s’agit de variables prépositionnées.

:point_right: Créez un nouveau script appelé "params.sh" contenant le code suivant.

```bash
#!/usr/bin/env bash

echo "Welcome $1! You are $2 years old." 
```

:point_right: Sauvegardez, rendez le script exécutable - avec `chmod +x` - et lancez-le en y ajoutant les paramètres `Vanessa` et `42`

```bash
./params.sh Vanessa 42
```

_Chaque argument est identifié par sa position : **$1** correspond au premier argument passé, **$2** au second et ainsi de suite..._

:blossom: N’hésitez pas à modifier les paramètres passés au script pour bien comprendre ce fonctionnement..

##### Interaction utilisateur

Il est possible de transmettre des valeurs à stocker dans des variables via les paramètres du script, il s’agit de variables prépositionnées.

:point_right: Créez un nouveau script appelé interact.sh contenant le code suivant

```bash
#!/usr/bin/env bash

echo "What is your name?"
read response
echo "Hello $response!"
```

:point_right: Sauvegardez, rendez le script exécutable - avec `chmod +x` - et lancez-le en y ajoutant un paramètre de votre choix (ex : Robert)

```bash
./interact.sh Robert
```

:point_right: Ajoutez une demande d'entrée (prompt) à l'utilisateur dans le fichier interact.sh

```bash
read -p "How old are you?" response
echo "You are $response years old"
```

:blossom: La commande Linux ci-dessus sert à interagir avec l'utilisateur en ligne de commande pour lui demander son âge, puis à afficher la réponse au lancement du script.

---

#### :bike: 3_Conditions & loops

##### Conditions

Selon le contenu d’une variable, il est possible d'exécuter certaines commandes à l’aide d’une condition if [...] then.

:point_right:  À l’aide de nano, créez un nouveau script appelé conditions.sh contenant le code suivant

```bash
#!/usr/bin/env bash

age=16
if [ $age -gt 18 ]
then
        echo "You are an adult"
else         
        echo "You are a minor"
fi
```

- Déterminez quel message sera affiché en lisant seulement le code ci-dessus.

> On définit une variable "age" contenant l’âge d’un utilisateur.  
> On regarde si le contenu de la variable "age" est plus grand que 18 ("gt" signifie "greater than")  
> Si c’est vrai, on affiche le message "You are an adult".  
> Sinon, on affiche le message "You are a minor".  

- Exécutez le sccript pour vérifier

- Mettez à jour le contenu de la variable "age" du script en remplaçant 16 par 42, puis exécutez le script

:point_right: Modifiez le script en ajoutant une condition intermédiaire "elif" avec le code suivant

```bash
#!/usr/bin/env bash

age=18
if [ $age -gt 18 ]
then         
        echo "You are an adult"
elif [ $age -eq 18 ] ; then
        echo "You have just reached majority"
else         
        echo "You are a minor"
fi
exit
```

:blossom: Exécutez ce script avec différentes valeur pour la variable `age` pour voir le résultat

##### Boucles

Une autre fonctionnalité utile lors de de l'exécution d’un script est la répétition d’une action, grâce à la syntaxe for [...] do.

:point_right: Créez un nouveau script appelé "loops.sh" contenant le code suivant.

```bash
#!/usr/bin/env bash

week="monday tuesday wednesday thursday friday saturday sunday"
for day in $week ; do
    echo "$day"
done
```

:blossom: Déterminez quel message sera affiché en lisant le code

> On définit une variable "week" contenant tous les jours de la semaine.  
> On parcourt les éléments de la variable semaine (le terminal sait que les espaces servent de délimitation entre 2 éléments) en les affectant à chaque tour de boucle à la variable "day".  
> À chaque tour de boucle, on affiche le contenu de la variable "day".  

:point_right: Sauvegardez, rendez le script exécutable - avec `chmod +x` - et lancez-le pour vérifier

---

#### :bike: 4_I love pets

##### Exécution de manière itérative

:point_right: Faites un script qui effectue les actions suivantes lorsqu'il est exécuté

- créer un tableau 'animals' contenant 5 éléments 'bear, pig, dog, cat, sheep'
- boucle sur chaque élément du tableau
- affiche l'élement courant

```bash
#!/usr/bin/env bash

animals=("bear" "pig" "dog" "cat" "sheep")
for animal in "${animals[@]}"
do
  echo $animal
done
```

---

#### :bike: 5_Folder or file?

##### Connaître le type d’un élément

:point_right: Créez un nouveau script appelé "checkType.sh" qui reçoit en argument un chemin d’accès et qui affiche le type de l’élément ciblé (dossier ou fichier).

- Si le script prend en entrée le chemin "/Users/antoine/Documents", le script affichera le message : "/Users/antoine/Documents is a directory"

- Si le script prend en entrée le chemin /Users/antoine/Documents/compta.docx, le script affichera "/Users/antoine/Documents/compta.docx is a regular file"

```bash
#!/usr/bin/env bash

USER_PATH=$1
if [ ! $USER_PATH ]; then
  echo "Path not specified"
exit 1
fi

# Syntaxe alternative
# if [ ! $USER_PATH ]
# then
# echo "Path not specified"
# exit 1
# fi

if [ ! -e $USER_PATH ]; then
  echo "$USER_PATH does not exists"
exit 1
fi
if [ -d $USER_PATH ]; then
  echo "$USER_PATH is a directory"
elif [ -f $USER_PATH ]; then
  echo "$USER_PATH is a regular file"
fi
```

##### Connaître le type de plusieurs éléments  

:point_right: Modifiez le script précédent pour qu’il accepte un nombre quelconque de chemins d’accès passés en argument à l’exécution. Le script devra afficher autant de messages que de chemins reçus.

```bash
#!/bin/bash

# Boucle sur tous les arguments passés au script
for USER_PATH in "$@"
do
  if [ ! "$USER_PATH" ]; then
    echo "Path not specified"
    exit 1
  fi

  if [ ! -e "$USER_PATH" ]; then
    echo "$USER_PATH does not exist"
    continue  # Passe au prochain chemin si celui-ci n'existe pas
  fi

  if [ -d "$USER_PATH" ]; then
    echo "$USER_PATH is a directory"
  elif [ -f "$USER_PATH" ]; then
    echo "$USER_PATH is a regular file"
  else
    echo "$USER_PATH is neither a regular file nor a directory"
  fi
done
```

---

#### :bike: 6_Play with permissions

##### Les permissions

Il peut arriver d’être limité dans une action par le terminal, car nous ne disposons pas des droits suffisants pour exécuter un script ou une commande système.

La commande **sudo** (superuser do) permet de pallier ce problème en donnant temporairement les droits d’administrateur à un utilisateur, via son mot de passe, afin que celui-ci puisse exécuter certaines commandes.

:point_right: Récupérez la ressource [playwithpermissions.zip](playwithpermissions.zip)

:point_right: Regardez dans le manuel (commande man) ce que permet de faire l’option "-l" de la commande ls, puis exécutez la commande suivante.

```bash
ls -l
```  

- Pour chaque fichier, vous obtenez une chaîne de caractères sous ce format

```bash
rw-r--r--
\ /\ /\ /
v  v  v
|  |  droits des autres utilisateurs (o)
|  |
|  droits des utilisateurs appartenant au groupe (g)
|
droits du propriétaire (u)

r : read | w : write | x : execute
```

- Vous constaterez que chaque fichier dispose de certaines permissions par défaut : le propriétaire (vous) peut lire et écrire dans ces fichiers tandis que les utilisateurs du groupe lié au fichier et tous les autres utilisateurs peuvent seulement les lire.

- La troisième et quatrième colonne représentent respectivement l’utilisateur et le groupe propriétaire du fichier.

##### Modification des permissions

Les permissions sont regroupées par paquets de 3 caractères (r, w, x ou un tiret). Imaginons qu’on souhaite modifier les permissions du propriétaire du fichier représentés par les 3 premiers caractères.

:point_right: Essayez d’exécuter le script "unexec.sh" grâce à la commande suivante.

```bash
./unexec.sh
```

Vous ne devrez pas être en mesure de pouvoir l’exécuter, car le propriétaire dispose seulement des droits en lecture et en écriture (les caractères r et w).

:point_right:  Modifiez les permissions du propriétaire (avec u=) grâce à la commande suivante.

```bash
chmod u=rwx unexec.sh
```

:point_right: Vérifiez la mise à jour des permissions grâce à la commande `ls -l` et vérifier que vous pouvez exécuter le script avec la commande `./unexec.sh`

##### Propriétaires et permissions

Intéressons-nous à l’influence entre les permissions et le droit de propriété d’un fichier.

:point_right: Modifiez le propriétaire du fichier "unexec.sh" en le remplaçant par l’utilisateur "nobody" (qui est un faux utilisateur déjà créé sur votre système) grâce à la commande suivante

```bash
sudo chown nobody unexec.sh
```

- Si vous essayez de lancer le script, vous ne devriez pas être en mesure de pouvoir l’exécuter, car vous n’êtes plus le propriétaire du fichier et le groupe (qui est inchangé et dont vous êtes membre) n’a pas les permissions d’exécution

:point_right: Modifiez les permissions du groupé lié au fichier (avec g=) grâce à la commande suivante

```bash
sudo chmod g=rx unexec.sh
```

:cool: Vous devriez pouvoir lancer le script désormais

> [!NOTE]
> Remarque : jusqu’à présent, pour rendre exécutable un script nous utilisions la commande chmod +x nomDuFichier. Cela permet de rendre le fichier exécutable quel que soit l’utilisateur courant en une seule commande.

---

#### :bike: 7_Easy permissions

##### Modification des propriétaires d’un ensemble de fichiers

Vous utiliserez l’utilitaire nano pour créer vos scripts afin de bénéficier d’un éditeur de texte intégré au terminal.
Pour créer et éditer un nouveau fichier, il suffit d’utiliser la commande suivante : nano nomDuFichier.extension.

:point_right: Récupérez la ressource [easypermissions.zip](easypermissions.zip)

:point_right: Créez l’utilisateur et le groupe "johncena" grâce aux commandes suivantes.

```bash
sudo useradd johncena
sudo groupadd johncena
```

:point_right: Ajoutez l’utilisateur "johncena" au groupe éponyme.

```bash
sudo usermod -aG johncena johncena
```

:point_right: Créez un script easyOwner.sh chargé de lire l’entrée du terminal (via la commande **read**) afin de récupérer le chemin vers un ou plusieurs fichiers, puis le nouveau propriétaire / groupe de ces fichiers.

- usage :
  
```bash
Files to update :
> file1 file2 file3

New owner and group :
> johncena

file1 owner changed to "johncena"
file2 owner changed to "johncena"
file3 owner changed to "johncena"
```

- le script

```bash
#!/usr/bin/env bash

read -p "Files to update :" CHEMINS
for FILE in $CHEMINS ; do
  read -p "New owner and group :" OWNER
  sudo chown $OWNER $FILE
  echo $FILE "owner changed to " $OWNER
done
exit
```

##### Modification des droits d’un ensemble de fichiers

:point_right: Créez un second script easyPermissions.sh chargé de lire l’entrée du terminal afin de récupérer le chemin vers un ou plusieurs fichiers, puis les nouvelles permissions au format "XXX", en suivant une [représentation en octal](https://askubuntu.com/questions/518259/understanding-chmod-symbolic-notation-and-use-of-octal/518260%23518260).

- usage
  
```bash
Files to update :
> file1 file2 file3

New permission :
> 444

file1 permissions changed to 444
file2 permissions changed to 444
```

- le script

```bash
#!/usr/bin/env bash

read -p "Files to update :" CHEMINS
for FILE in $CHEMINS ; do
  read -p "New permissions Octal :" PERMISSION 
  sudo chmod $PERMISSION $FILE
  echo $FILE "permissions changed to " $PERMISSION 
done
exit
```

---

#### :bike: 8_Permissions checker

##### Vérification des droits d’exécution d’un fichier

:point_right:  Créez un script "checkPermissions.sh" prenant en paramètre un chemin d’accès vers un fichier afin de vérifier s’il existe et ses permissions.

- Si le fichier n’existe pas, le message suivant sera affiché : "FILE does not exist"

- Si l’utilisateur actuel dispose des droits d’exécutions sur le fichier, le message suivant sera affiché : "You have permissions to execute FILE" sinon "You do not have permissions to execute FILE".

```bash
#!/bin/bash

# Vérifier si un argument a été fourni
if [ "$#" -ne 1 ]; then
  echo "Usage: $0 <file_path>"
  exit 1
fi
# Obtenir le chemin du fichier à partir des arguments
FILE=$1
# Vérifier si le fichier existe
if [ ! -e "$FILE" ]; then
  echo "$FILE does not exist"
  exit 1
fi
# Vérifier les permissions d'exécution du fichier pour l'utilisateur
actuel
if [ -x "$FILE" ]; then
  echo "You have permissions to execute $FILE"
else
  echo "You do not have permissions to execute $FILE"
fi
```

---

#### :bike: 9_Count files

##### Compter le nombre de fichiers par utilisateur

:point_right:   Créez un script "countFiles.sh" qui prend en paramètre un chemin d’accès vers un dossier afin d’afficher le nombre de fichiers contenus dans le répertoire pour chaque propriétaire.

Exemple de réponse :

```bash
root 1
user1 2
user2 5
nobody 1
```

- le code correspondant :

```bash
#!/bin/bash

# Vérifier si un argument a été fourni
if [ -z "$1" ]; then
  echo "Veuillez fournir un chemin de répertoire."
exit 1
fi

# Vérifier si le chemin fourni est un répertoire
if [ ! -d "$1" ]; then
  echo "Le chemin spécifié n'est pas un répertoire."
exit 1
fi

# Compter les fichiers par utilisateur
find "$1" -type f -exec ls -l {} \; | awk '{print $3}' | sort | uniq -c |
awk '{print $2, $1}'
```

---

#### :bike: 11_Vacation pictures

##### Formatage des noms de fichiers

:point_right: Créez un nouveau script appelé "renameFiles.sh" chargé de renommer les fichiers portant l’extension .jpg (et seulement ces fichiers) contenus dans le répertoire "picturesToRename".

- Les fichiers devront porter le nom suivant : YYYY-MM-DD-nomDuFichier.jpeg où "YYYY-MM-DD" correspond à la date du jour au format année-mois-jour et "nomDuFichier" au nom original du fichier avant d’être renommé.

- Les fichiers renommés devront être déplacés dans le répertoire "renamedPictures", sans altérer les fichiers originaux.

_Par exemple : Si nous sommes le 2 juin 2050 et que le script traite le fichier "picturesToRename/beach.jpg", il sera renommé en "renamedPictures/2050-06-02-beach.jpg"._

```bash
#!/usr/bin/env bash

# Renommer les fichiers avec la date

DAY=$(date +%F)

cd picturesToRename
for FILE in *.jpg; do
  echo "Renaming $FILE to $DAY-$FILE"
  cp $FILE "../renamedPictures/$DAY-$FILE"
done
```

:point_right: Modifiez le script précédent pour qu’il renomme tous les fichiers présents dans "renamedPictures" selon un type d’extension indiqué par l’utilisateur en argument.

_Par exemple : Si l’utilisateur exécute le script avec la commande ./renameFiles.sh png, tous les fichiers présents dans le dossier "renamedPictures" auront l’extension .png._

```bash
#!/usr/bin/env bash

# Renommer les fichiers avec la date

DAY=$(date +%F)

cd picturesToRename
for FILE in *.jpg; do
  echo "Renaming $FILE to $DAY-$FILE"
  cp $FILE "../renamedPictures/$DAY-$FILE"
done

# Renommer les fichiers avec une extension reçue en argument
NEW_EXTENSION=$1
if [ ! $NEW_EXTENSION ]; then
  echo "No need to change extensions"
  exit 0
fi

cd ../renamedPictures
echo "Changing .jpg to $NEW_EXTENSION..."

for FILE in *; do
  NEW_FILE=$(echo $FILE | sed "s|.jpg|$NEW_EXTENSION|")
  echo "Renaming $FILE to $NEW_FILE"
  mv $FILE $NEW_FILE
done
```

---

#### :bike: 12_Back in 10 minutes

##### Création d'un script

:point_right: Dans le dossier "/home/engineer/cron" créez un nouveau fichier nommé “mon_script.sh” qui devra ajouter le texte "Hello, this script is running!" dans le fichier "/home/engineer/logs/log.log"

```bash
#!/bin/bash

dir=/home/engineer/logs
mkdir -p $dir

filename=$dir/log.log
test -f $filename || touch $filename

echo "Hello, this script is running!" >> “$filename”
```

:floppy_disk: Sauvegardez le script et rendez-le exécutable.

:mag_right: Vous pouvez maintenant tester votre script en le lançant et en vérifiant le contenu du fichier log.log

```bash
./monscript.sh

cat ./logs/log.log
```

##### Automatisation avec crontab

Crontab ou cron est comme un assistant pour effectuer des tâches répétitives sur un système informatique. Il fonctionne en arrière-plan, ce qu'on appelle un "daemon". Ce service attend patiemment jusqu'à des moments précis définis dans un fichier de configuration (appelé crontab), puis il exécute des actions spécifiques, comme des sauvegardes ou des scripts, et se rendort jusqu'au prochain événement prévu.

:information_source: Consultez le manuel de crontab avec `man crontab`

:point_right: Ouvrez le fichier cron et introduisez une instruction qui exécutera le script mon_script.sh toutes les 10 minutes.

```bash
# Ouvrir l'édition de crontab
crontab -e
```

```bash
# Ajouter la ligne suivante, sauvegardez et quitter l'éditeur
*/10 * * * * /home/engineer/cron/mon_script.sh
```

```bash
# Vérifier les conr-jobs
crontab -l
```

#### :bike: 13_Auto Backup

##### Préparation

:point_right: Créez tout d’abord le fichier “ma_donnee_importante.txt” dans le dossier “/home/engineer/data”.

```bash
touch ma_donnee_importante.txt
```

:point_right: Créez un nouveau script “mon_backup.sh” qui fera le backup du fichier que vous venez de créer dans un dossier de backup.

Le backup devra se faire dans le dossier “/home/engineer/backup/”

Pour chaque itération, un timestamp (horodatage) devra être ajouté au nom du fichier sauvegardé.

En fonction de la variable d’environnement ENV_TYPE, le backup se placera dans le sous-dossier “dev”, “preprod” ou “prod”.

Si la valeur est différente ou si la variable n’est pas définie, un message d’erreur devra être renvoyé.

```bash
#!/bin/bash

if [ -z "$ENV_TYPE" ]; then
  echo "Error : ENV_TYPE is undefined."
  exit 1
fi

case "$ENV_TYPE" in
  dev)
    backup_dir="/home/engineer/backup/dev"
    ;;
  preprod)
    backup_dir="/home/engineer/backup/preprod"
    ;;
  prod)
    backup_dir="/home/engineer/backup/prod"
    ;;
  *)
    echo "Error : ENV_TYPE has unsupported value."
    exit 1
    ;;
esac

timestamp=$(date +"%Y%m%d_%H%M%S")

mkdir -p $backup_dir

cp /home/engineer/ma_donnee_importante.txt "$backup_dir/fichier_$timestamp"
```

:floppy_disk: Sauvegardez le script et rendez-le exécutable.

##### Automatisation du backup

:point_right: Définissez la variable d’environnement à “dev”

```bash
export ENV_TYPE="dev"
```

:point_right: Ouvrez le fichier cron et introduisez une instruction qui exécutera le script mon_backup.sh toutes les 5 minutes.

```bash
*/5 * * * * /chemin/vers/votre/script/mon_backup.sh
```

:mag: Vérifier que la tâche est bien enregistrée avec `crontab -e`

:mag: Attendez quelques minutes et vérifiez si votre script s'est exécuté en consultant le dossier de backup “dev”.

:mag:  Modifiez la variable d'environnement à “preprod”, attendez quelques minutes et vérifiez si votre script s'est exécuté en consultant le dossier de backup “preprod”.

:mag: Modifiez la variable d'environnement à “prod”, attendez quelques minutes et vérifiez si votre script s'est exécuté en consultant le dossier de backup “prod”.

:mag: Modifiez la variable d'environnement à “test”, attendez quelques minutes... il n'ya pas de dossier test ! Vérifiez les logs de crontab avec la commande suivante :

```bash
sudo journalctl -u cron.service
```

Vous constaterez une erreur

```bash
(CRON) info (No MTA installed, discarding output)
```

:information_source: Ce message apparaît parce que cron n'a pas trouvé de MTA (Mail Transfert Agent) configuré sur le système pour envoyer l'email avec la sortie du job, donc il a simplement ignoré la sortie.

##### Capturer les erreurs

L’erreur que vous avez renvoyée dans votre script n’est visible nulle part, il va falloir capturer l’erreur au moment de l’exécution de votre script et la renvoyer vers un fichier.

:point_right: Dans votre configuration de crontab, trouvez un moyen pour renvoyer les outputs (echo) de votre script vers un fichier de logs “/home/engineer/logs/cron.log”. Au bout de quelques instants, un fichier cron.log sera créé dans le répertoire “/home/engineer/logs”.

```bash
*/5 * * * * /chemin/vers/votre/script/mon_backup.sh >> /home/engineer/logs/cron.log 2>&1
```

- 2>&1 signifie "rediriger le flux d'erreur (stderr) vers le flux de sortie standard (stdout)".

  1 : Le flux de sortie standard (stdout). C'est là où les messages normaux de sortie d'un programme sont envoyés.

  2 : Le flux de sortie d'erreur standard (stderr). C'est là où les messages d'erreur d'un programme sont envoyés.

:warning: **N'oubliez pas de supprimer la tâche cron du fichier avec `crontab -e`**