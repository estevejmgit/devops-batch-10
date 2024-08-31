   # Formation devOps
_La capsule_

:fire: Exercices et corrections formation devOps :fire:

---
## Semaine 1 :computer: 

Bases du fonctionnement des outils informatiques - Terminal, scripts, notion de serveur backend 

### Jour 2 : Scripting & Droits Linux

---

#### :bike: 1_Execute my script

##### <ins> Création d’un premier script </ins>

Vous utiliserez l’utilitaire nano pour créer vos scripts afin de bénéficier d’un éditeur de texte intégré au terminal.
Pour créer et éditer un nouveau fichier, il suffit d’utiliser la commande suivante : nano nomDuFichier.extension.

:point_right:  Exécutez la commande `nano myscript.sh` et copiez le code suivant dans la fenêtre de l’éditeur de texte :

```bash
#!/usr/bin/env bash

echo "Hello world!"
```

:keyboard: Sauvegardez le fichier en appuyant sur les touches `CTRL + X`, puis en appuyant sur `y` (yes) et enfin sur `Enter`.

##### <ins> Exécution d’un script </ins>

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

##### <ins> Variables simples </ins>

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

##### <ins> Variables d’environnement </ins>

Les variables permettent de stocker des valeurs et de les réutiliser ou de les mettre à jour en y faisant appel.

Il existe également des variables définies de manière globale au sein de votre terminal, on les appelle variables d’environnement et celles-ci contiennent des informations utiles pouvant être transmises aux processus de votre session shell.

:point_right: Depuis votre terminal, exécutez la commande `printenv HOME`.

_Cette commande retourne le chemin d’accès vers le répertoire par défaut de votre terminal qui devrait ressembler à ça :_

```bash
/home/engineer
```

:blossom: Affichez la liste de toutes les variables d’environnement avec la commande `printenv`.

##### <ins> Variables prépositionnées </ins>

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

##### <ins> Interaction utilisateur </ins>

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

##### <ins> Conditions </ins>

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

##### <ins> Boucles </ins>
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

##### <ins> Exécution de manière itérative </ins>

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

##### <ins> Connaître le type d’un élément </ins>

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

##### <ins> Connaître le type de plusieurs éléments  </ins>

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

##### <ins> Les permissions </ins>

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

-  La troisième et quatrième colonne représentent respectivement l’utilisateur et le groupe propriétaire du fichier.

##### <ins> Modification des permissions </ins>

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


##### <ins> Propriétaires et permissions </ins>

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

_Vous devriez pouvoir lancer le script désormais_

> [!NOTE]
> Remarque : jusqu’à présent, pour rendre exécutable un script nous utilisions la commande chmod +x nomDuFichier. Cela permet de rendre le fichier exécutable quel que soit l’utilisateur courant en une seule commande.


---

#### :bike: 7_Easy permissions

##### <ins> Modification des propriétaires d’un ensemble de fichiers </ins>

Vous utiliserez l’utilitaire nano pour créer vos scripts afin de bénéficier d’un éditeur de texte intégré au terminal.
Pour créer et éditer un nouveau fichier, il suffit d’utiliser la commande suivante : nano nomDuFichier.extension.

:point_right:  Récupérez la ressource [easypermissions.zip](easypermissions.zip)

```bash
#!/usr/bin/env bash

echo "Hello world!"
```

:keyboard: Sauvegardez le fichier en appuyant sur les touches `CTRL + X`, puis en appuyant sur `y` (yes) et enfin sur `Enter`.

##### <ins> Exécution d’un script </ins>

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
