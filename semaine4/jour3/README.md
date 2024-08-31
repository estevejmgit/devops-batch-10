# Formation devOps
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

## Semaine 4

:tanabata_tree: Déploiement continu, tests de déploiement, Provider Cloud Azure DevOps 

### Jour 3 : Qualité et sécurité du code ###

---

#### :bike: 1_Sonar Cube Begin

[SonarQube](https://www.sonarqube.org/) est un logiciel open source de gestion de qualité et sécurité du code, principalement utilisé pour inspecter le code source d’applications en développement afin de détecter des bugs, des vulnérabilités de sécurité ou d’autres anomalies pouvant nuire à la qualité du code source et donc au bon fonctionnement de l’application.

##### <ins> Pré-requis </ins>

La mise en place de SonarQube a pour objectif d’aider les développeurs à créer un code de meilleure qualité en pointant 
les problèmes et en proposant des solutions adéquates pour près de 29 langages de programmation.

:point_right: Commencez par installer Java 11 qui est requis pour le lancement de SonarQube.

```bash
sudo apt install default-jdk
```

Check installed version

```bash
java --version
```

:point_right: Installer sonarQube

Suivez la [documentation](https://docs.sonarqube.org/latest/setup/get-started-2-minutes/) d’installation de SonarQube afin 
de télécharger et extraire l’archive zip de la "Community Edition".

1 télécharger [SonarQube Community Edition zip file](https://www.sonarqube.org/downloads/). 

2 As a **non-root user**, unzip it in /opt/sonarqube (change sonarqube/ ownership for current user if sudo was used to unzip). 

3 As a **non-root user**, to start sonarqube execute :  ```/opt/sonarqube/<SONAR_FILE>/bin/<OS>/sonar.sh console```

exemple for ubuntu 22.04 / sonarqube 10.6.0.92116 :  
> PATH = /opt/sonarqube/sonarqube-10.6.0.92116/bin/linux-x86-64/


```
/opt/sonarqube/sonarqube-10.6.0.92116/bin/linux-x86-64/sonar.sh console
```

> [!WARNING]
> La première isntall peut prendre jusque 3 minutes !


:point_right:  Une fois que l’instance est démarrée et fonctionnelle, visitez l’interface de SonarQube en utilisant les 
informations données dans la documentation.

```
http://localhost:9000
```

login : admin | mdp : admin > Changed to 4dmin

_L’instance est désormais prête à être utilisée, mais à des fins pédagogiques seulement._
_En effet, une instance utilisée pour un vrai projet professionnel doit normalement être installée sur un_
_serveur dans le cloud pour des raisons d'accessibilité et de performance._



##### <ins> Scanner un projet local </ins>


:point_right:  Install Scanner

- Depuis l’interface de SonarQube, créé un projet local nommé "CovidTracker" avec "CT" comme clé de projet > **use the global setting**.

👉 Sélectionnez l’analyse de projet en local et suivez les instructions afin de générer un *token* et télécharger l’outil en ligne de commande *sonar-scanner*.
_Vous pouvez ignorer l’instruction qui demande d’ajouter le répertoire "bin" dans le "PATH"._


- Dans sonarqube http://localhost:9000 :

👉 Run analysis : choisir "Other (PHP, JS, Go,  Python)" puis "Linux" (si on est sur linux bien-sûr) 

👉 Download the Scanner for Linux : \
Visit the official [documentation](https://docs.sonarsource.com/sonarqube/10.6/analyzing-source-code/scanners/sonarscanner/) 
of the Scanner (opens in new tab) to download the latest version

- Dans la console :

```
Unzip <path_to_scanner> /opt/sonarqube/
```

:point_right:  Install local project

Clonez le répertoire GitHub du projet open source CovidTracker : https://github.com/CovidTrackerFr/covidtracker-web \
Positionnez vous dans le dossier "covidtracker-web" 

```
git clone <git repo>
cd covidetracker-web
```

👉 Grâce à la documentation et la notion de chemin absolu, exécutez la CLI de sonar-scanner afin de scanner le projet CovidTracker via SonarQube.

```
/opt/sonarqube/sonar-scanner-<VERSION>/sonar-scanner \
  -Dsonar.projectKey=CT \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.token=<YOUR_TOKEN>
```

> [!WARNING]
> Sonar n'aime pas les path avec des underscore "_". Dans le projet covid il y a un path _data qui pose problème : il faut le renommer data/
> il reste des erreurs lors de l'analyse mais le resultat du test est bien affiché

Une fois l’analyse terminée, vous êtes censés voir les résultats de l’analyse sur le dashboard de SonarQube.

Vous pouvez voir que de nombreux bugs sont détectés : cela ne signifie pas que l’application ne fonctionne pas en l’état, mais cela énumère plutôt chaque bug potentiel sur chaque ligne de code et pour chaque fichier analysé (ce qui explique le grand nombre de bugs détectés)

👉 Parcourez le résultat du scan et filtrez les bugs détectés par "Severity" afin de ne récupérer que le bug considéré comme critique par SonarQube.


---
#### :bike: 2_Sonarqube Meets Gitlab

##### <ins> Install </ins>

Maintenant que vous avez découvert le concept de qualité et sécurité du code dans un environnement local, il est temps d’aller plus loin en intégrant cette vérification dans une pipeline d’intégration continue via une instance SonarQube dans le cloud, grâce à [SonarCloud](https://www.sonarsource.com/products/sonarcloud/).

👉 Créez un compte sur SonarCloud. Attention : Il faut importer vos organisations et créer un [token Gitlab](https://gitlab.com/-/user_settings/personal_access_tokens)

👉 Reprenez le repository GitLab "pokedex" issu du challenge "Deploy to Vercel" et assurez-vous que l’intégralité du code source est identique sur les branches "main" et "prod". N’hésitez pas à repartir d’un nouveau repository GitLab si besoin.

👉 Vérifiez que la mise en production sur [Vercel](https://vercel.com) ne se fait qu’à partir de la branche "prod"

<mark>Projects pages > pokedexProj > Settings > GIT > production branch : "prod"</mark>

👉 Modifiez la visibilité du projet sur GitLab en le passant en public.

_Cette étape est obligatoire pour pouvoir utiliser SonarCloud dans sa version gratuite._

<mark>Repo > Settings > General : Visibility, project features & permissions</mark>



##### <ins> Integration SonarQubue </ins>

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

```yaml
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
```


👉 Avant de lancer la première analyse et à partir de la branche "main", modifiez le fichier ".gitlab-ci.yml" afin que l’analyse du code via SonarQube ne soit effectuée que lors d’une merge request vers la branche "main" (et non pas lors d’une merge request vers "prod", par exemple). Ajoutez l'option 'only', à la même indentation que 'script':

```yaml
  only:
    - main
```

👉 Créez un nouveau projet depuis sonarQube


**commandes de lancement à partir de la racine du projet pokedex**

```bash
<PATH_TO_SCANNER>/sonar-scanner \
  -Dsonar.projectKey=pokedex \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.token=<TOKEN>
```

_Changez les valeurs de < PATH_TO_SCANNER > et < TOKEN >_

**Push and check Gitlab > repo > pokedex  & sonarCloud > project > pokedex**

Pushez votre code : Après quelques minutes, vous êtes censés obtenir un résumé de l’analyse de la branche principale,


**Modifications, push et merge request**

👉 Mettez vous dans la peau d’un développeur quelques instants en créant une nouvelle branche "codequality" (toujours à partir de "main") où vous devrez régler les bugs rapportés par SonarQube, notamment sur les fichiers "index.html" et "style.css".

👉 Une fois les bugs réglés, lancez une nouvelle analyse de SonarQube en créant une merge request afin de fusionner la branche "codequality" dans la branche "main".

👉 Finissez par créer une merge request pour la branche "main" vers la branche "prod" afin de mettre en production l’application vers Vercel.
