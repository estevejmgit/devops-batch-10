**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

**Semaine 3 - GIT JIRA et CI**

**Jour 3 : CI**

---

# 6 - Maximum Weight

## <ins> Pipeline de vérification v2 </ins>

Ce challenge va vous permettre de créer un nouveau job qui sera en erreur si un des fichiers qui a été commit 
dépasse une certaine taille, paramétrable directement depuis GitLab.

👉 Repartez du répertoire GitLab utilisé dans le challenge précédent, changez le nom du job dans le yaml:

```
check_api:
  stage: test
  script:
    - echo "$(date +%u)"
```

pour check_friday

```
check_friday:
  stage: test
  script:
    - echo "$(date +%u)"
```


👉 Depuis l’interface GitLab, créez une variable personnalisée nommée "MAXIMUM_WEIGHT" qui a pour valeur "2M" (pour 2 megabytes ou MB)

_Sur la page projet de gitlab, menu gauche > settgings > CI /CD, puis 'expand' la partie variables_


👉 Créez un script "checkSize.sh" recevant une taille maximum en argument (par exemple 12M pour 12 megabytes) afin de 
lister les fichiers excédant cette taille maximum.

./checkSize 12M
./doc.pdf 13M
./videos/demo.mp4 24M

```
#!/bin/bash

# Vérifie si un argument a été passé
if [ -z "$1" ]; then
  echo "Usage: $0 <maximum_size>"
  exit 1
fi

MAX_SIZE=$1
EXCEEDING_FILES=$(find . -type f -size +"$MAX_SIZE")

# Vérifie s'il y a des fichiers qui dépassent la taille maximale
if [ -n "$EXCEEDING_FILES" ]; then
  echo "Des fichiers dépassent la taille maximale de $MAX_SIZE :"
  exit 1
else
  echo "Aucun fichier ne dépasse la taille maximale de $MAX_SIZE."
fi
```

👉 Créez un job chargé d’exécuter le script précédemment créé en passant la variable personnalisée "MAXIMUM_WEIGHT" en tant qu'argument.

La pipeline est censée être en erreur si un fichier ou plus excède la taille paramétrée depuis GitLab.

```
stages:
  - test

variables:
  API_URL: "https://jsonplaceholder.typicode.com/users"

max_weight:
  stage: test
  script:
    - echo "Check Size"
    - echo $MAXIMUM_WEIGHT
    - chmod +x checkSize.sh
    - ./checkSize.sh "$MAXIMUM_WEIGHT"
```

👉 Testez le job en créant un fichier de 5 MB via la commande dd et poussez-le vers le dépot de distant.
La pipeline est censée échouer car le fichier excède la limite de 2 MB.

```
dd if=/dev/null of=wont_pass.file bs=1k seek=51200
```

