**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

**Semaine 3 - GIT JIRA et CI**

**Jour 3 : CI**

---

# 2 - Last Commit

## <ins> varibles prédéfinies </ins>

L’objectif de ce challenge est de récupérer et exploiter les informations d’un commit lors de l’exécution d’une pipeline : 
ID de commit, auteur, fichiers modifiés, etc.

👉 Reprenez le répertoire du challenge précédent et supprimez le contenu du fichier ".gitlab-ci.yml".

👉 Grâce à la notion de [variables prédéfinies](https://docs.gitlab.com/ee/ci/variables/) avec GitLab, créez un job 
"displayinfos" chargé d’afficher les infos suivantes :

- L’auteur du commit au format "Name <email>"
- L’ID du commit (au format SHA raccourci de 8 caractères)
- La liste des fichiers modifiés depuis le dernier commit

```
stages:
  - test

job:
  stage: test
  script:
    - echo "Hello World !"
    - echo $CI_COMMIT_AUTHOR
    - echo $CI_COMMIT_SHORT_SHA
    - echo $CI_COMMIT_BEFORE_SHA
    - echo $CI_COMMIT_SHA
    - echo "Modified files:"
    - git diff-tree -r --name-only $CI_COMMIT_BEFORE_SHA $CI_COMMIT_SHA
```


👉 Créez un nouveau script shell nommé "checkAuthor.sh" recevant un paramètre l’auteur d’un commit au format "Name <email>".

Si l’email de l’auteur contient bien "@", afficher "Valid address", sinon afficher "Invalid address" et 
terminer le script avec l’instruction "exit 1".

_checkAuthor.sh_

```
#!/bin/bash

# Vérifie si un paramètre a été passé
if [ -z "$1" ]; then
  echo "Usage: $0 \"NAME <EMAIL>\""
  exit 1
fi

# Extraction de l'email
EMAIL=$(echo "$1" | grep -oP '(?<=<).*(?=>)')

# Vérifie si l'email contient "@"
if [[ "$EMAIL" == *"@"* ]]; then
  echo "Valid address"
else
  echo "Invalid address"
  exit 1
fi
```


👉 Faites en sorte qu'il se déclanche lors vos prochains pushes.

_Rendez le script exécuatble_

```
chmod +x checkAuthor.sh
```

_Refaites le yaml pour dire à la CI d'exécuter le sccript_

```
stages:
  - test

job:
  stage: test
  script:
    - echo "Author would be:"
    - echo $CI_COMMIT_AUTHOR
    - echo "Modified files:"
    - git diff-tree -r --name-only $CI_COMMIT_BEFORE_SHA $CI_COMMIT_SHA
    - ./checkAuthor.sh "$CI_COMMIT_AUTHOR"
```

👉 Changez la condition de vérification de l'email pour arriver sur une erreur lors de l'exécution de la CI


