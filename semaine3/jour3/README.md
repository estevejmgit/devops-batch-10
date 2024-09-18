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

#### :bike: API checker

##### Merge requests & pipelines

#### :bike: Friday Alarm

##### Pipeline de vérification

#### :bike: Maximum Weight

##### Pipeline de vérification V2

