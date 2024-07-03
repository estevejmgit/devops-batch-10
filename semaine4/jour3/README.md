# Formation devOps
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

## Semaine 4

### Jour 3 : Qualité et sécurité du code ###

---

**1 - SONARQUBE BEGIN**



[ ] <ins>### Install ###</ins>

[SonarQube](https://www.sonarqube.org/) est un logiciel open source de gestion de qualité et sécurité du code, principalement utilisé pour inspecter 
le code source d’applications en développement afin de détecter des bugs, des vulnérabilités de sécurité ou d’autres 
anomalies pouvant nuire à la qualité du code source et donc au bon fonctionnement de l’application.

La mise en place de SonarQube a pour objectif d’aider les développeurs à créer un code de meilleure qualité en pointant 
les problèmes et en proposant des solutions adéquates pour près de 29 langages de programmation.

👉 Commencez par installer Java 11 qui est requis pour le lancement de SonarQube.

```
sudo apt install default-jdk
```

Check installed version

```
java --version
```

👉 Suivez la [documentation](https://docs.sonarqube.org/latest/setup/get-started-2-minutes/) d’installation de SonarQube afin 
de télécharger et extraire l’archive zip de la "Community Edition".

1 télécharger [SonarQube Community Edition zip file](https://www.sonarqube.org/downloads/). 

2 As a **non-root user**, unzip it in, for example, /opt/sonarqube (change sonarqube/ folder ownership accordingly). 

3 As a **non-root user**, to start sonarqube execute :  /opt/sonarqube/<PATH>/bin/<OS>/sonar.sh console


_change \<OS\> and \<PATH\> for your OS and installed PATH reference :

_ex ubuntu 22.04 / sonarqube 10.6.0.92116 : PATH = /opt/sonarqube/sonarqube-10.6.0.92116/bin/linux-x86-64/ | OS = linux-x86-64_


```
/opt/sonarqube/sonarqube-10.6.0.92116/bin/linux-x86-64/sonar.sh console
```

> [!WARNING]
> La première isntall peut prendre jusque 3 minutes !


👉 Une fois que l’instance est démarrée et fonctionnelle, visitez l’interface de SonarQube en utilisant les 
informations données dans la documentation.

```
http://localhost:9000
```

login : admin | mdp : admin > Changed to 4dmin

_L’instance est désormais prête à être utilisée, mais à des fins pédagogiques seulement._
_En effet, une instance utilisée pour un vrai projet professionnel doit normalement être installée sur un_
_serveur dans le cloud pour des raisons d'accessibilité et de performance._



[ ] <ins>### Scanner un projet local ###</ins>


**Install Scanner**

👉 Depuis l’interface de SonarQube, créé un projet local nommé "CovidTracker" avec "CT" comme clé de projet > **use the global setting**.

👉 Sélectionnez l’analyse de projet en local et suivez les instructions afin de **générer un token** et télécharger l’outil en ligne de commande **sonar-scanner**.
_Vous pouvez ignorer l’instruction qui demande d’ajouter le répertoire "bin" dans le "PATH"._


Dans sonarqube http://localhost:9000 :

1 Run analysis : choisir "Other (PHP, JS, Go,  Python)" puis "Linux" (si on est sur linux bien-sûr) 

2 Download the Scanner for Linux : \
Visit the official [documentation](https://docs.sonarsource.com/sonarqube/10.6/analyzing-source-code/scanners/sonarscanner/) 
of the Scanner (opens in new tab) to download the latest version


Dans la console :

3 Unzip scanner in /opt/sonarqube/


**Install local project**

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


**1 - SONARQUBE MEETS GITLAB**



[ ] <ins>### Install ###</ins>

Maintenant que vous avez découvert le concept de qualité et sécurité du code dans un environnement local, il est temps d’aller plus loin en intégrant cette vérification dans une pipeline d’intégration continue via une instance SonarQube dans le cloud, grâce à [SonarCloud](https://www.sonarsource.com/products/sonarcloud/).

👉 Créez un compte sur SonarCloud.

👉 Reprenez le repository GitLab "pokedex" issu du challenge "Deploy to Vercel" et assurez-vous que l’intégralité du code source est identique sur les branches "main" et "prod". N’hésitez pas à repartir d’un nouveau repository GitLab si besoin.

👉 Vérifiez que la mise en production sur Vercel ne se fait qu’à partir de la branche "prod"

<mark>Projects pages > pokedexProj > Settings > GIT > production branch : "prod"</mark>

👉 Modifiez la visibilité du projet sur GitLab en le passant en public.
_Cette étape est obligatoire pour pouvoir utiliser SonarCloud dans sa version gratuite._

<mark>Repo > Settings > General : Visibility, project features & permissions</mark>