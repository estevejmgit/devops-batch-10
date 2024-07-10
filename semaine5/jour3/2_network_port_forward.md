**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

**Semaine 5 - Containers et orchestration**

**Jour 3 : Kubernetes**

---

# 2 - NETWORK & PORT FORWARDING

## Reseau avec Kubernetes

*👉 Via la commande kubectl run, démarrez un pod nommé "httpd-server" contenant un seul conteneur, 
basé sur l’image officielle de httpd et en exposant le port 80.

```
kubectl run myapache --image=httpd:latest --port=80
```

👉 À partir de la documentation de kubectl, trouvez une commande permettant d’obtenir
toutes les informations détaillées d’une ressource Kubernetes et exécutez-là afin de 
décrire le pod "httpd-server".

```
kubectl get pod -o wide #(detail sur tt les pods)
kubectl describe pods #(affiche tt les pods)
kubectl describe pods/<POD NAME>
```

👉 Grâce à la commande précédente, vous êtes censé pouvoir récupérer l’adresse IP locale du pod. Tentez de faire une requête HTTP via curl à partir de cette adresse.

```
curl http://172.17.X.X
```

**La requête n’aboutit pas ? C’est tout à fait normal ! Rappelez-vous que les conteneurs Docker sont isolés, y compris au niveau du réseau.**

C’est le même principe pour Kubernetes : les conteneurs inclus dans un pod peuvent communiquer entre eux, mais il faut explicitement rediriger (forward) un port de la machine hôte vers un conteneur afin de communiquer avec lui, y compris si le port en question a déjà été exposé lors de la création du pod.

👉 Afin de mieux comprendre le fonctionnement de l’isolation réseau de Kubernetes, trouvez une commande permettant de rediriger le port 8080 de la machine hôte vers le port 80 du conteneur "httpd-server”.

```
kubectl port-forward pods/<POD NAME> 8080:80
```
