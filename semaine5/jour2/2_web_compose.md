**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

**Semaine 5**

**Jour 2 : Docker Compose**

---

# 2 - ADVANCED DOCKERFILE

👉 Créez un nouveau fichier "docker-compose.yml" contenant un service nommé "nginx" basé sur 
l’image nginx:stable en exposant le port d’écoute par défaut du serveur web pour qu’il soit joignable 
depuis le port 8080 sur la machine hôte.

```
services:
  nginx:
    image: nginx:stable
    ports:
      - 8080:80
```

👉 Arrêtez le service et supprimez le conteneur lié via la commande docker compose down.

```
docker compose down
docker ps -a
docker container rm <CONTAINER NAME/ID>
```

👉 Reprendre l’image "nginx-lacapsule" du challenge de la veille "Advanced Dockerfile" afin de remplacer 
l’image nginx:stable par cette dernière.

_Dockerfile :_ (même arbo que docker-compose.yml)

```
FROM nginx:stable

EXPOSE 81
```

Modifier _docker-compose.yml_

```
services:
  nginx:
    build: .
    ports:
      - 8080:81
```
