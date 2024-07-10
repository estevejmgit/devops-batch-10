**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

**Semaine 5 - Containers et orchestration**

**Jour 3 : Kubernetes**

---

# 5 - ALL ROLLING UPDATES

## 1 - Start Roll Update

👉 Créez et appliquez un manifeste de déploiement en vous assurant que les contraintes suivantes soient respectées :

- Le nom de l’application déployée sera "rollingapp"
- Le nom du manifeste sera "rollingapp-deployment"
- Le conteneur déployé sera nommé "nginx-hello", basé sur l’image "nginxdemos/hello" dans sa dernière version et devra exposer le port 80
- 3 pods devront être utilisés pour le déploiement du conteneur "nginx-hello"

```
apiVersion: apps/v1

kind: Deployment
metadata:
  name: rollingapp-deployment
  labels:
    app: rollingapp
spec:
  replicas: 3
  selector:
    matchLabels:
      app: rollingapp
  template:
    metadata:
      labels:
        app: rollingapp
    spec:
      containers:
      - name: nginx-hello
        image: nginxdemos/hello:latest
        imagePullPolicy: Always
        ports:
        - containerPort: 80
```

👉 Créez et appliquez un service dédié au load balancing de l’application "rollingapp" déployée précédemment.

```
apiVersion: v1

kind: Service
metadata:
  name: rollingapp-service
  labels:
    app: rollingapp

spec:
  type: LoadBalancer
  ports:
  - name: http
    port: 8080
    protocol: TCP
    targetPort: 80
  selector:
    app: rollingapp
  sessionAffinity: None
```

👉 Consultez la documentation pour la commande kubectl set afin de procéder à une mise à jour de l’application déployée 
en modifiant l’image utilisée par les conteneurs "nginx-hello". La nouvelle version à déployée est basée sur une autre 
version de la même image taguée "plain-text".

> kubectl set image deployment/\<DEPLOY METADATA NAME\> \<CONTAINER NAME\>=\<IMAGE NAME\>

```
kubectl set image deployhment/rollingapp-deployment nginx-hello=nginxdemos/hello:plaintext
```

_Si vous vérifiez la liste des pods pendant que la mise à jour est déployée, vous constaterez que les "anciens" pods sont petit à petit 
supprimés pour laisser place à des nouveaux dotés de conteneurs basés sur la nouvelle version de l’image._

👉 Vérifiez les informations détaillées de tous les pods en une seule commande afin de vérifier que chacun héberge bien un conteneur basé 
sur l’image "nginxdemos/hello:plain-text". 

```
kubectl describe pods
```

_Vous commencez à vous rendre compte que Kubernetes est un véritable must-have pour la gestion et le déploiement de conteneurs d’applications, surtout à grande échelle._

Imaginez le contexte suivant : suite au déploiement d’une nouvelle version, les développeurs se rendent compte qu’une fonctionnalité n’a pas été recettée (vérifiée) en profondeur et qu’une mise à jour vers la version précédente doit être faite de toute urgence…

👉 Trouvez la commande permettant de revenir sur une version précédente du déploiement et annuler la dernière mise à jour, sans utiliser la commande kubectl set image.

```
kubectl rollout undo deployments/rollingapp-deployment
``

👉 Vérifiez les informations détaillées de tous les pods (en une seule commande) afin de vérifier que chacun héberge bien un conteneur basé sur l’image "nginxdemos/hello:latest".


```
kubectl describe pods
```
