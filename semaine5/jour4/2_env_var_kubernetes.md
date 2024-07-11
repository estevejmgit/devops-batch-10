**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

**Semaine 5**

**Jour 4 : Kubernetes Avancé**

---

# 2 - ENV VAR ET KUBERNETES

## Setup

👉 Créez un manifeste de déploiement en vous assurant que les contraintes suivantes soient respectées :


    Le nom de l’application déployée sera "motd"
    Le nom du manifeste sera "motd-deployment"
    Le conteneur déployé sera nommé "alpine" et basé sur l’image alpine dans sa dernière version
    5 pods devront être utilisés pour le déploiement du conteneur "alpine"

```
kubectl apply -f motd-deployment.yml --namespace=webapp-prod
```
_Si vous tentez d’appliquer ce manifeste de déploiement, vos pods seront en erreur et c’est tout à fait normal : le conteneur
basé sur l’image alpine s’arrête après son lancement, car il n’a aucune action à effectuer._



