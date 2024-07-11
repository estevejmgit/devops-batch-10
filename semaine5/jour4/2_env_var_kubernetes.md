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


De la même façon qu’il existe des manifestes pour le déploiement et pour les services, la configuration des variables d’environnement peut également se faire avec un simple fichier grâce au concept de ConfigMaps.

👉 Créez un fichier nommé "motd-config.yml" contenant le manifeste suivant.

```
apiVersion: v1

kind: ConfigMap
metadata:
  name: motd-config
  labels:
    app: motd
data:
  MESSAGE: "Hi i'm a simple container inside a pod"
  OTHER_MESSAGE: "You can't see me!"
```

__Si vous prenez le temps d’analyser ce fichier, vous pouvez voir que les metadata sont semblables à un manifeste de déploiement et que les variables d’environnement sont simplement définies dans la tableau "data"._

👉 Appliquez ce manifeste grâce à la commande habituelle donnée ci-dessous.

```
kubectl apply -f motd-config.yml
``

👉 Trouvez la commande kubectl capable d’afficher tous les manifestes ConfigMaps du cluster afin de vérifier que "motd-config" a bien été créé.
