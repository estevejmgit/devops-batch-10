# Formation devOps

:pill: La capsule

:fire:  Documentation d'accompagnement au cycle devOps :fire:

---

**Semaine 5 - Containers et orchestration**

**Jour 3 : Kubernetes**

---

# 3 - DEPLOY MY PODS

## 1 - Manifest Creation

Jusqu’à maintenant, vous avez pu déployer un pod contenant un seul conteneur via Kubernetes (avec kubectl) et soyons honnête, à part quelques différences au niveau de la syntaxe et de la rapidité de déploiement, rien de bien révolutionnaire par rapport à Docker !

Mais ne vous inquiétez pas, les choses sérieuses commencent avec ce challenge qui va vous permettre de vous confronter à l’équivalent du fichier Docker Compose version Kubernetes, mais surtout à la notion de scaling de ressources.

👉 Créez un fichier nommé "httpd-server-deployment.yml" et insérez le manifeste ci-dessous. Ce fichier permet de décrire la stratégie de déploiement d’un conteneur basé sur l’image httpd.

```
apiVersion: apps/v1

kind: Deployment
metadata:
  name: httpd-server-deployment
  labels:
    app: httpd-server

spec:
  replicas: 1
  selector:
    matchLabels:
      app: httpd-server
  template:
    metadata:
      labels:
        app: httpd-server
    spec:
      containers:
      - name: httpd-server
        image: httpd:latest
        imagePullPolicy: Always
```

👉 Appliquez ce manifeste grâce à la commande ci-dessous.

```
kubectl apply -f httpd-server-deployment.yml
```

👉 Trouvez l’option à appliquer à la commande kubectl get afin de vérifier l’état des déploiements.

```
kubectl get deployments
```

👉 Modifiez le fichier créé précédemment et dédié au déploiement de l’application "httpd-server" afin d’exposer le port 80.

```
    spec:
      containers:
      - name: httpd-server
        image: httpd:latest
        imagePullPolicy: Always
        ports:
        - containerport: 80
```


👉 Appliquez la modification apportée au manifeste via la commande kubectl apply.

```
kubectl apply -f httpd-server-deployment.yml
```

👉 Comme vu dans le challenge précédent, redirigez le port 8080 de la machine hôte vers le port 80 du conteneur httpd-server.

```
kubectl port-forward pods/<POD NAME> 8080:80
```

Prenez le temps de vérifier le nom du pod créé lors du déploiement via la commande kubectl get pods.

👉 Gardez ouvert le terminal où la commande précédente a été exécutée et à partir d’un nouveau terminal, tentez une requête HTTP via curl sur localhost (ou 127.0.0.1), en précisant le port 8080.

```
curl -v http://localhost:8080
```

## 2 - Manifest MODIF !

Dans certains cas, vous n’aurez pas la possibilité d’utiliser VSCode pour modifier un manifeste de déploiement, car la machine hôte utilisée ne dispose pas d’interface graphique (GUI).

Sachez qu’il existe deux modes de création des ressources Kubernetes :

    Le mode déclaratif utilisant ce qu’on appelle des manifestes écrit en YAML, c’est ce que vous avez fait jusqu’à maintenant
    Le mode impératif créant et modifiant les ressources à la volée, c’est ce que vous allez faire plus tard dans ce challenge


👉 Trouvez une commande kubectl permettant d’éditer rapidement le manifeste un déploiement en mode impératif, sans avoir à mettre à jour le fichier YAML directement.

```
kubectl edit deployment/httpd-server-deployment
```

⚠️ Attention : les modifications apportées via kubectl seront directement appliquées, mais ne seront pas répercutées sur le fichier "httpd-server-deployment.yml".

👉 Après avoir exécuté la commande précédente, modifiez le manifeste afin de déployer le conteneur "httpd-server" sur 4 pods distincts au lieu d’un seul.

L’éditeur par défaut sera vim, il est un peu particulier car compliqué à prendre en main de prime abord, mais c’est l’occasion de prendre en main l’un des "concurrents" de nano.

👉 À l’ouverture, l'éditeur vim est en mode "lecture seule", pressez la touche "i" pour passer en mode INSERT.

👉 Une fois vos modifications terminées, appuyez sur "Echap" pour repasser en mode "lecture seule", puis saisissez la commande ":wq" afin de sauvegarder le fichier et quitter l’éditeur.

👉 Vérifiez la création des 4 pods grâce à la commande kubectl get pods.



## 3 - Scaling PODS

Dans un environnement de production, ces 4 pods seront répartis entre les différents workers disponibles.
Ainsi, dans l’éventualité d’un crash d’un conteneur ou d’un worker HS, le reste des pods pourront prendre le relais.

👉 Trouvez une commande kubectl permettant changer le nombre de pods déployés (replicas) à 2 en mode impératif, sans modifier directement le manifeste de déploiement.


```
kubectl edit deployment/httpd-server-deployment
```

👉 Pour finir, trouvez la commande permettant de supprimer un déploiement.
Cette commande est également censée supprimer les pods liés au déploiement.
```
kubectl delete deployment/<DEPLOYMENT NAME>
```

