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

#### :bike: Flake8

##### Test d’intégration continue

#### :bike: API checker

##### Merge requests & pipelines

#### :bike: Friday Alarm

##### Pipeline de vérification

#### :bike: Maximum Weight

##### Pipeline de vérification V2

