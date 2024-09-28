# Formation devOps

:pill: La capsule

:fire:  Documentation d'accompagnement au cycle devOps :fire:

---

## Semaine 5 :pager: 

Docker, Docker compose et Kubernetes pour faire tourner les containers !

### Jour 2 : Compose

#### :bike: Hello World !

##### Découverte de Docker et Docker Compose

Si vous avez installé la dernière version de Docker précédement (_2.29.x as of today_), il y a des chances que Docker Compose soit déjà installé, vous pouvez le vérifier en lançant la commande 

```bash
docker compose version 
```

:warning: Différence entre ```docker-compose``` (v1) et ```docker compose``` (v2) : la nouvelle syntaxe de l'outil Docker Compose dans sa V2 enlève le ```-``` entre ```docker``` et ```compose```

si ```docker compose version``` ne renvoie rien c'est qu'il n'est pas installé [voir cette doc](https://netshopisp.medium.com/how-to-install-docker-compose-on-debian-12-server-a0414293dbdf) 

:point_right: Créez un fichier "docker-compose.yml" censé créer un service (conteneur) lançant l’image "hello-world".  
~~L’instruction "version" permet de spécifier la version du fichier Docker Compose qu’on souhaite utiliser~~ (déprécié)

```yaml
services:
  helloworld:
    image: "hello-world:latest"
```
> on peut le lancer avec <mark>docker compose up</mark> avec l'option <mark>-d</mark> pour _detached_, lancer le container en tâche de fond.


```bash
docker-compose up -d
```

:point_right: Afin de vous entraîner à manipuler le fichier Docker Compose, ajoutez un second service nommé "helloworld2" et basé sur la même image que le premier service.

```yaml
services:
  helloworld:
    image: "hello-world:latest"
  helloworld2:
    image: "hello-world:latest"
```

> pour lancer un seul servicce du yaml : <mark>docker compose up helloworld2</mark>


