# Formation devOps

:pill: La capsule

:fire:  Documentation d'accompagnement au cycle devOps :fire:

---

## Semaine 3 :zap:

Versionning avancé avec Git, Jira et intégration continue et tests d'intégration

### Jour 3 : Intergration continue

#### :bike: You had one job

##### Création d’une pipeline

:point_right: En vous inspirant de la [documentation](https://docs.gitlab.com/ee/ci/yaml/gitlab_ci_yaml.html) de GitLab et à partir de VS Code, créez un fichier ".gitlab-ci.yml" basique content un seul [stage](https://docs.gitlab.com/ee/ci/pipelines/) nommé "test" et contenant un job "say-hello" chargé de faire une simple commande : echo "Hello world!".

```yaml
stages:
    - test

say-hello:       # job name !
    stage: test  # stage du job
    script:
      - echo "Hello world!"
```

##### Configuration d’une pipeline

:point_right: Trouvez un moyen de lancer le job "say-hello" uniquement lors d’un push sur la branche
"development" et testez ces changements en créant une branche en local puis en la poussant
vers GitLab.

```yaml
stages:
    - test

say-hello:       # job name !
    stage: test  # stage du job
    rules:       # conditions d'exécution
        - if: '$CI_COMMIT_BRANCH == "development"'
    script:
        - echo "Hello world!"
```

#### :bike: Last Commit

##### Variables prédéfinies & pipelines

:point_right: Grâce à la notion de [variables prédéfinies](https://docs.gitlab.com/ee/ci/variables/) avec GitLab, créez un job "displayinfos" chargé d’afficher les infos suivantes :

- L’auteur du commit au format "Name <email>"
- L’ID du commit (au format SHA raccourci de 8 caractères)
- La liste des fichiers modifiés depuis le dernier commit

```yaml
display-infos:
    script:
        - echo $CI_COMMIT_AUTHOR
        - echo $CI_COMMIT_SHORT_SHA
        - git diff-tree --no-commit-id --name-only -r $CI_COMMIT_SHA
```

- ```git diff-tree``` : Affiche les différences entre deux arbres Git. Cela peut être utilisé pour comparer l'état d'un commit par rapport à son parent.

- ```--no-commit-id``` : Ne montre pas l'ID du commit dans la sortie. Par défaut, git diff-tree afficherait aussi l'identifiant du commit comparé, mais ici on ne veut pas ça.

- ```--name-only``` : Affiche uniquement les noms des fichiers qui ont été modifiés, sans afficher les détails des modifications.

- ```-r``` : Recurse dans tous les sous-répertoires pour s'assurer que la commande s'applique récursivement à tout l'arborescence des fichiers du commit.

- ````$CI_COMMIT_SHA```` : Représente le hash du commit que l'on veut inspecter. Cette variable est souvent utilisée dans les pipelines CI/CD (comme avec GitLab CI) pour désigner le commit en cours de traitement.

:point_right: Créez un nouveau script shell nommé "checkAuthor.sh" recevant un paramètre l’auteur d’un
commit au format "Name <email>".

Si l’email de l’auteur contient bien "@", afficher "Valid address", sinon afficher "Invalid address"
et terminer le script avec l’instruction "exit 1".

```bash
#!/usr/bin/env bash

if [[ $1 == *@* ]]; then
    echo "Valid address"
else
    echo "Invalid address"
    exit 1
fi
```

:point_right: Modifiez le fichier "gitlab-ci.yml" afin de créer un nouveau job "check-author" dans le stage
"test" afin d’exécuter le script créé précédemment en lui passant la variable prédéfinie
**$CI_COMMIT_AUTHOR** en guise d’argument.

```yaml
stages:
    - test

check-author:
    stage: test
    script:
        - chmod +x checkAuthor.sh
        - ./checkAuthor.sh "$CI_COMMIT_AUTHOR"
```

#### :bike: Flake8

##### Test d’intégration continue

:point_right: Faites en sorte d’exécuter le linter [Flake8](https://flake8.pycqa.org/) lors d’un push sur n’importe quelle branche.

Pour ce faire, vous aurez sans doute besoin d’utiliser la [notion d’image](https://docs.gitlab.com/ee/ci/docker/using_docker_images.html) afin de lancer un job dans un environnement spécifique (avec Python pré-installé, par exemple 😉)

```yaml
image: "python:3.9"

stages:
- test

linter:
    stage: test
    script:
        - python -m pip install flake8
        - flake8
```

:point_right: Même si c’est plutôt le rôle des développeurs, modifiez le code afin de ne plus avoir
d’erreurs du linter.

Veillez à ne pas supprimer la ligne "import os", mais plutôt l’ignorer via flake8.

```yaml
import os # noqa

# bloc fonction
def print_length(str):
    print(len(str))
# fin bloc fonction

print_length("Hello world!")
```

:warning: c'est le commentaire ```# noqa``` qui permet à flake8 d'ignorer la ligne

#### :bike: API checker

##### Merge requests & pipelines

:point_right: Sur la branche principale, créez un fichier ".gitlab-ci.yml" qui devra exécuter un job chargé
de vérifier qu’une API (potentiellement utilisée dans le projet) est bien joignable afin de valider
l’exécution de la pipeline.

Vous pouvez choisir la "fausse" [API JSONPlaceholder](https://jsonplaceholder.typicode.com/) et l’endpoint "GET /users"

```yaml
stages:
    - test
api-checker:
    stage: test
    script:
        - curl https://jsonplaceholder.typicode.com/users
```

:warning: Pour rendre les merge-requests dépendant du succès des pipeline pour le projet :

- Aller à la racine de votre dépôt gitlab
- (menu de gauche) Settings > Merge Requests 
- Cochez l'option "Pipelines must succeed"

#### :bike: Friday Alarm

##### Pipeline de vérification

:point_right: En repartant du répertoire créé dans le challenge précédent créez un nouveau job qui sera
en erreur si le commit a lieu un vendredi.

La demande de merge request est donc censée se bloquer automatiquement si elle est faite
un vendredi, car vous découvrez (ou connaissez) l’adage : on ne met pas un production un
vendredi !

```yaml
stages:
    - test
friday-alarm:
    stage: test
    script:
        - if [[ $(date +%u) -eq 5 ]]; then exit 1; fi
```

- ```$(date +%u)``` :

    Cette partie exécute la commande date avec l'option +%u.
    date +%u renvoie le jour actuel de la semaine sous forme numérique (1 pour lundi, 2 pour mardi, etc., jusqu'à 7 pour dimanche).
    Par exemple, si aujourd'hui c'est vendredi, $(date +%u) retournera 5.

- ```-eq 5``` :

    Cette expression teste si la valeur retournée par $(date +%u) est égale à 5.
    Donc, cela vérifie si le jour actuel est vendredi.

- ```if [[ ... ]]; then ... fi``` :

    C'est une structure conditionnelle en Bash.
    Si la condition à l'intérieur des doubles crochets ```[[ ... ]]``` est vraie, alors la commande après then est exécutée. Sinon, elle est ignorée.

- ```exit 1``` :

    Si la condition est remplie (c'est-à-dire si c'est vendredi), la commande exit 1 sera exécutée.
    Cela force le script à se terminer immédiatement avec un code d'erreur 1. (En général, dans Linux, un code de sortie différent de 0 signifie une erreur ou une condition d'arrêt).

#### :bike: Maximum Weight

##### Pipeline de vérification V2

- Récupérez les fichiers du challenge dans ressource

:point_right: Créez un script "checkSize.sh" recevant une taille maximum en argument (par exemple
12M pour 12 megabytes) afin de lister les fichiers excédant cette taille maximum.

```bash
#!/usr/bin/env bash

files=$(find . -type f -size +$1)

if [[ ! -z $files ]]; then
    find . -type f -size +$1 -exec ls -lh {} \; | awk '{ print $9 " " $5 }'
    exit 1
fi
```

- ```#!/usr/bin/env bash```

    La première ligne est une shebang qui indique au système d'utiliser l'interpréteur bash pour exécuter ce script. Cela garantit que le script sera exécuté avec bash quel que soit l'emplacement de l'interpréteur sur le système.

- ```files=$(find . -type f -size +$1)```

    Cette ligne utilise la commande find pour rechercher des fichiers (-type f) dans le répertoire courant (.) qui ont une taille supérieure à celle spécifiée dans l'argument $1 (exemple : 100k, 1M pour 1 mégaoctet, etc.).
    Le résultat de cette commande est assigné à la variable files.

- ```if [[ ! -z $files ]]; then```

    Cette condition vérifie si la variable $files n'est pas vide (autrement dit, si des fichiers correspondants ont été trouvés).
    La condition [[ ! -z $files ]] est vraie si files contient au moins un fichier trouvé.

- ```find . -type f -size +$1 -exec ls -lh {} ; | awk '{ print $9 " " $5 }'```

    Si des fichiers ont été trouvés, cette commande find est exécutée à nouveau pour trouver les fichiers ayant une taille supérieure à $1.

    L'option -exec ls -lh {} \; permet d'exécuter la commande ls -lh sur chaque fichier trouvé. Cette commande ls -lh affiche les fichiers avec des détails en format long, notamment la taille en un format lisible par l'humain (par exemple, en Ko, Mo, Go).

    La sortie de ls -lh est ensuite passée à la commande awk, qui filtre et affiche uniquement le nom du fichier (champ 9) et la taille du fichier (champ 5). Cela permet de ne pas afficher d'autres informations comme les droits, le propriétaire, etc.

- ```exit 1```

    Enfin, le script se termine avec un code de sortie 1 qui indique une erreur ou une condition non standard (ici, cela pourrait signifier que des fichiers trop gros ont été trouvés).

:point_right:  Créez un job chargé d’exécuter le script précédemment créé en passant _la variable
personnalisée_ "MAXIMUM_WEIGHT" en tant qu'argument.
La pipeline est censée être en erreur si un fichier ou plus excède la taille paramétrée depuis
GitLab.

```yaml
stages:
    - test

check-size:
    stage: test
    script:
        - chmod +x checkSize.sh
        - ./checkSize.sh $MAXIMUM_WEIGHT
```

:warning: Déclarer la variable et sa valeur dans les varible d'environnement de la pipeline sur gitlab !
