**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

**Semaine 5 - Containers et orchestration**

**Jour 3 : Kubernetes**

---

# 4 - SERVICE LOAD BALANCER

## 1 - SetUp

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

## 2 - Notion de service

Comme vu dans les challenges précédents, la commande kubectl port-forward permet de binder un port d’un conteneur sur la machine hôte, ce qui est utile pour comprendre le fonctionnement de Kubernetes et s'entraîner, mais pas vraiment adapté dans un environnement de production.

En effet, la notion de service avec Kubernetes sera plus adaptée car elle permettra de rendre disponible une application web sur internet, mais également de rediriger le trafic équitablement entre les pods afin de répartir la charge, c’est ce que l’on appelle un load balancer.

👉 Créez un nouveau fichier nommé "mywebserver-service.yml" et complétez le service ci-dessous afin de l’adapter à votre déploiement précédemment créé.

```
apiVersion: v1

kind: Service
metadata:
  name: mws-service
  labels:
    app: mywebserver

spec:
  type: LoadBalancer
  ports:
  - name: http
    port: 8080
    protocol: TCP
    targetPort: 80
  selector:
    app: mywebserver
  sessionAffinity: None
```

👉 Trouvez l’option à appliquer à la commande kubectl get afin de vérifier l’état des services.

