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
kubectl describe pods #(affiche tt les pods)
kubectl describe pods/<POD NAME>
```
