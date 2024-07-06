**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

**Semaine 4**

**Jour 3 : Qualité et sécurité du code**

---

# 3 - XSS VULNERABILITY

## <ins> Install </ins>

_Vous n’êtes pas sans savoir qu’en plus d’analyser les bugs dans le code source d’une application, SonarQube est capable d’analyser les vulnérabilités qui peuvent être critiques pour la sûreté des utilisateurs et de leurs données._

A travers ce challenge vous allez récupérer une application de tchat qui peut paraître toute simple de prime abord, mais qui semble cacher d’importantes failles de sécurité. Saurez-vous les détecter et les régler ?

👉 Récupérez la ressource "xssvulnerability.zip" depuis [l’url sur Ariane](https://static.lacapsule.academy/programs/devops-full-time/J21/xssvulnerability.zip).

👉 Commencez par installer les dépendances de cette application Node.js via l’utilitaire en ligne de commande yarn DEPUIS LE DOSSIER RACINE DU PROJET.

```
yarn install && yarn start
```

👉 Essayez l’application pendant quelques instants puis versionnez-la sur un nouveau repository GitLab nommé "simple-chat". 



## <ins> Analyse des Vulnérabilités </ins>

👉 Avant la mise en place d’une pipeline d’intégration continue, lancez une analyse via une instance locale de SonarQube.


Une fois l’analyse terminée, le rapport semble mettre en avant un "Security Hotspot", c’est-à-dire une potentielle faille de sécurité qui pourrait être exploitée par des hackers afin de nuire à votre application !


👉 Tentez d’exploiter la faille rapportée par SonarQube en tapant directement un message dans le tchat.

> [!NOTICE]
> Une certaine commande "/date" semble exécuter la commande du même nom côté serveur. 

Pourquoi ne pas tenter d'enchaîner avec une autre commande Linux ?

<mark>/date && whoami</mark>


👉 Créez une nouvelle branche nommée "hotfix" afin de soumettre une nouvelle version du code source responsable de la vulnérabilité via une merge request.

Dans server.js :

```
// const cmdResponse = cp.execSync(cmd).toString();
cp.spawnSync("/usr/bin/file.exe", { shell: false }); // Compliant
```

**_Lors de la création de la merge request, ne cochez pas l’option permettant de supprimer la branche d’origine._**


👉 Maintenant que l’application semble sûre, mettez en place un nouveau job chargé de l’analyse du code source de 
l’application via SonarCloud, uniquement lors d’une merge request vers la branche principale du dépôt.

suivre les même steps que <ins>### Integration SonarQubue ###</ins> sur le site de http://sonrcloud.io


👉 Créez un second job afin de déployer l’application en production via le service Vercel (comme vu il y a quelques jours) lors d’un nouveau commit sur la branche "main".
Vercel s’occupera de créer une pipeline externe, nul besoin de modifier le fichier ".gitlab-ci.yml"

> il semble qu'il y ai un pb : sur vercel avec fichier io
