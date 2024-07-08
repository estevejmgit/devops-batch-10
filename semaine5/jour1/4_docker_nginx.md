**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

**Semaine 5**

**Jour 1 : Conteneurisation**

---

# 4 - DOCKER ET NGINX

## <ins> Docker, nginx et ports </ins>

👉 Levez un conteneur Docker nommé "cont-nginx" basé sur l’image officielle de nginx : https://hub.docker.com/_/nginx 
Attention, à l’inverse de l’image debian, vous devrez lever le conteneur en mode détaché (via l’option -d) afin qu’il puisse se démarrer en tâche de fond.

```
docker run -it -d --name cont-nginx nginx:latest
```
> A ce stade, le container est lancé mais n'est pas joingable car aucun ports n'a été spécifié

👉 Supprimez le conteneur précédemment créé et re-créez en un nouveau avec l’option -p en précisant le port que l’on souhaite "bind" sur la machine hôte ainsi que le port cible.

_docker run -d -p \<HOST_PORT\>:\<CONT_PORT\> --name \<GIVE_CONT_NAME\> \<IMG_NAME\>_

```
docker stop cont-nginx
docker container rm cont-nginx
docker run -d -p 8080:80 --name cont-nginx nginx
```


## <ins> Les logs de nginx via docker </ins>

👉 Dans la documentation des commandes Docker, trouvez la commande et l’option vous permettant de consulter les logs du conteneur en temps réel. Essayez de faire une nouvelle requête afin de voir si elle est affichée dans les logs.

```
docker logs -f cont-nginx
```


