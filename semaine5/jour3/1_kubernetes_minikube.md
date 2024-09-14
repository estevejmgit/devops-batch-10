# Formation devOps

:pill: La capsule

:fire:  Documentation d'accompagnement au cycle devOps :fire:

---

**Semaine 5 - Containers et orchestration**

**Jour 3 : Kubernetes**

---

# 1 - INSTALL MINIKUBE

Installer le minikube [selon la doc](https://minikube.sigs.k8s.io/docs/start/?arch=%2Flinux%2Fx86-64%2Fstable%2Fbinary+download)

```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64
```

**_Check l'install_**

```
minikube version
```

**Installer _kubectl_**

```
curl -LO https://dl.k8s.io/release/$(curl -Ls https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
```

**start minikube**

``` 
minikube start
```

# 2 - START POD

```
kubectl run myfirstpod --image=hello-world:latest
```

Un pod permet de rassembler différents conteneurs liés à une application ou un environnement.
Cette notion vient remplacer celle de Docker Compose avec les services puisque Kubernetes permettra d’orchestrer différents conteneurs d’une façon bien plus poussée et "production ready".

👉 Exécutez la commande suivante afin d’obtenir la liste des pods liés au cluster.

```
kubectl get pods
```

La commande kubectl communique directement avec le "master node" qui se charge à son tour de communiquer avec les workers nodes qui contiennent les fameux pods.

Dans votre cas, Minikube simule cette architecture avec un master node et un seul worker sur la même machine, mais en production chaque partie est une machine à part entière.

👉 Trouvez la commande permettant de récupérer les logs d’un pod précis.

```
kubectl logs myfirstpod
```

👉 Enfin, supprimez le pod créé précédemment.

```
kubectl delete pods myfirstpod
```

Le pod créé dans ce challenge ne contenait qu’un seul container, mais il ne s’agit que d’un exemple pour prendre un main la CLI de kubectl.

Dans un contexte de production et de haute disponibilité, Kubernetes permet d'orchestrer un cluster constitué de nombreux pods, contenant chacun les mêmes conteneurs.
