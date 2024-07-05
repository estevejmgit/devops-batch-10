# Formation devOps
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

## Semaine 4

### Jour 4 : Azure devOps ###

**2 - ARTEFACTS EN OPTION**

---

[ ] <ins>### Commencer par les bases ###</ins>

👉 Créez un nouveau projet nommé : “Weather Forecast”.

👉 Accédez à l'onglet "Repos" et créez un nouveau repository Git vide.

👉 Clonez ce [repository github](https://github.com/Adedoyin-Emmanuel/react-weather-app) sur votre ordinateur.

>NB : changer git remote rm origin / git remote add origin <git@REPO CREE CI-DESSUS>

👉 Envoyez le projet React sur Azure DevOps.

> _Alternativement on peut importer directement sur Azure le repo github et le cloner en local depuis azure (Attention au default branch name)_

---

[ ] <ins>### Enregistrer les artifacts ###</ins>

👉 Créez un fichier azure-pipelines.yml dans la racine de votre projet ReactJS.

👉 Configurez le pipeline pour installer les dépendances, packager les node_modules et les enregistrer comme artefacts.

NB : il faut faire un npm install puis regarder dans la doc azure publish artifacts :

```
trigger:
- master

pool:
 name: 'python-sample-pool'

steps:
- script: npm install 
# - script: tar -czf node_modules.tar.gz node_modules

- task: PublishPipelineArtifact@1
  inputs:
    # targetPath: '$(Pipeline.Workspace)'
    targetPath: 'node_modules'
    publishLocation: 'pipeline'
    artifact: 'drop'
```

---

[ ] <ins>### Enregistrer les artifacts ###</ins>


👉 Ajoutez une étape dans le pipeline pour <mark>déployer l'application</mark> ReactJS sur votre VM en utilisant les artefacts générés.


> [!TIP]
> Pour utiliser les Artefacts ajouter :
```
steps:
- download: current
  artifact: drop
  patterns: |
    **/*.js
```

> Pour déployer l'aPP, voire ci-dessus <mark>Lancer le projet sur votre VM (????)</mark>

---
