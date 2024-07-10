**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

**Semaine 5 - Containers et orchestration**

**Jour 3 : Kubernetes**

---

# 4 - SERVICE LOAD BALANCER

👉 Créez un manifeste "mywebserver-deployment.yml" dédié à un déploiement de pods en suivant les 
contraintes suivantes :

- Le nom de l’application déployée sera "mywebserver"  
- Le nom du manifeste de déploiement sera "mws-deployment"  
- Le conteneur déployé sera nommé "nginx-hello", basé sur l’image nginxdemos/hello
dans sa dernière version et devra exposer le port 80  
- 5 pods devront être utilisés pour le déploiement du conteneur "nginx-hello"  

```
apiVersion: apps/v1

kind: Deployment
metadata:
  name: mws-deployment
  labels:
    app: mywebserver
spec:
  replicas: 5
  selector:
    matchLabels:
      app: mywebserver
  template:
    metadata:
      labels:
        app: mywebserver
    spec:
      containers:
      - name: nginx-hello
        image: nginxdemos/hello:latest
        imagePullPolicy: Always
        ports:
        - containerPort: 80
``` 

👉 Appliquez le manifeste créé précédemment afin de déployer les pods contenant chacun un seul conteneur "nginx-hello".

```
kubectl apply -f mywebserver-deployment.yml
```
