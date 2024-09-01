**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

**Semaine 4**

**Jour 3 : Qualité et sécurité du code**

---

# 2 - SONARQUBE MEETS GITLAB


## Install 

Maintenant que vous avez découvert le concept de qualité et sécurité du code dans un environnement local, il est temps d’aller plus loin en intégrant cette vérification dans une pipeline d’intégration continue via une instance SonarQube dans le cloud, grâce à [SonarCloud](https://www.sonarsource.com/products/sonarcloud/).

👉 Créez un compte sur SonarCloud. Attention : Il faut importer vos organisations et créer un [token Gitlab](https://gitlab.com/-/user_settings/personal_access_tokens)

👉 Reprenez le repository GitLab "pokedex" issu du challenge "Deploy to Vercel" et assurez-vous que l’intégralité du code source est identique sur les branches "main" et "prod". N’hésitez pas à repartir d’un nouveau repository GitLab si besoin.

👉 Vérifiez que la mise en production sur [Vercel](https://vercel.com) ne se fait qu’à partir de la branche "prod"

<mark>Projects pages > pokedexProj > Settings > GIT > production branch : "prod"</mark>

👉 Modifiez la visibilité du projet sur GitLab en le passant en public.
_Cette étape est obligatoire pour pouvoir utiliser SonarCloud dans sa version gratuite._

<mark>Repo > Settings > General : Visibility, project features & permissions</mark>



## Integration SonarQubue 

👉 À partir de l’interface de SonarCloud, créez un nouveau projet nommé "Pokedex" et suivez scrupuleusement les étapes (en les adaptant si nécessaire) pour mettre en place l’analyse du code source du dépôt.

<mark>Choisir "Analyze a project with GitLab CI/CD Pipeline" et suivre les instructions :</mark>


**Add environement variable**

<ins>a. Define the SonarCloud Token environment variable</ins>

In GitLab, go to Settings > CI/CD > Variables to add the following variable and make sure it is available for your project:

- In the Key field, enter SONAR_TOKEN

- In the Value field, enter \<GIVEN TOKEN\>

_Make sure that the Protect variable checkbox is unticked_

_Make sure that the Mask variable checkbox is ticked_


<ins>b. Define the SonarCloud URL environment variable</ins>

Still in Settings > CI/CD > Variables add a new variable and make sure it is available for your project:

- In the Key field, enter SONAR_HOST_URL

- In the Value field, enter https://sonarcloud.io 

_Make sure that the Protect variable checkbox is unticked_

_No need to tick the Mask variable checkbox this time_


**Create a .gitlab-ci.yml**

```
variables:
  SONAR_USER_HOME: "${CI_PROJECT_DIR}/.sonar"  # Defines the location of the analysis task cache
  GIT_DEPTH: "0"  # Tells git to fetch all the branches of the project, required by the analysis task
sonarcloud-check:
  image:
    name: sonarsource/sonar-scanner-cli:latest
    entrypoint: [""]
  cache:
    key: "${CI_JOB_NAME}"
    paths:
      - .sonar/cache
  script:
    - sonar-scanner
  only:
    - merge_requests
    - master
    - develop
```


👉 Avant de lancer la première analyse et à partir de la branche "main", modifiez le fichier ".gitlab-ci.yml" afin que l’analyse du code via SonarQube ne soit effectuée que lors d’une merge request vers la branche "main" (et non pas lors d’une merge request vers "prod", par exemple).

```
only:
  - merge_requests
  - main
```

👉 Créez un nouveau projet depuis sonarQube


**commandes de lancement à partir de la racine du projet pokedex**

```
\<PATH_TO\>/sonar-scanner \
  -Dsonar.projectKey=pokedex \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.token=\<TOKEN\>
```

**Push and check Gitlab > repo > pokedex  & sonarCloud > project > pokedex**

Pushez votre code : Après quelques minutes, vous êtes censés obtenir un résumé de l’analyse de la branche principale,


**Modifications, push et merge request**

👉 Mettez vous dans la peau d’un développeur quelques instants en créant une nouvelle branche "codequality" (toujours à partir de "main") où vous devrez régler les bugs rapportés par SonarQube, notamment sur les fichiers "index.html" et "style.css".

👉 Une fois les bugs réglés, lancez une nouvelle analyse de SonarQube en créant une merge request afin de fusionner la branche "codequality" dans la branche "main".

👉 Finissez par créer une merge request pour la branche "main" vers la branche "prod" afin de mettre en production l’application vers Vercel.
