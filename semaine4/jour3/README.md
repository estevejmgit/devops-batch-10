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
