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
docker compose up -d
```

:point_right: Pour **arrêter** les containers lancés avec Compose

```bash
docker compose stop
```

:point_right: Pour **supprimer** les containers

```bash
docker compose down
```

:point_right: Pour supprimer les containers ET les volumes persistants

```bash
docker compose down -v
```

:point_right: Afin de vous entraîner à manipuler le fichier Docker Compose, ajoutez un second service nommé "helloworld2" et basé sur la même image que le premier service puis lancez le docker compose

```yaml
services:
  helloworld:
    image: "hello-world:latest"
  helloworld2:
    image: "hello-world:latest"
```

> pour lancer un seul service du yaml : ```docker compose up helloworld2```

> pour lister les services lancés : ```docker compose ps```

#### :bike: Web Compose

:point_right: Créez un nouveau fichier "docker-compose.yml" contenant un service nommé "nginx" basé sur 
l’image nginx:stable en exposant le port d’écoute par défaut du serveur web pour qu’il soit joignable 
depuis le port 8080 sur la machine hôte.

```yaml
services:
  nginx:
    image: nginx:stable
    ports:
      - 8080:80
```

:point_right: Démarrez le service "nginx" et vérifiez le lancement du service avec une requête curl.


```bash
docker-compose up -d
curl -v http://localhost:8080
```

:point_right: Arrêtez le service et supprimez le conteneur lié via la commande docker compose down.

```bash
docker compose down
docker ps -a
docker container rm <CONTAINER NAME/ID>
```

:point_right: Reprendre l’image "nginx-lacapsule" du challenge de la veille "Advanced Dockerfile" afin de remplacer 
l’image nginx:stable par cette dernière.

_Dockerfile :_ (même arbo que docker-compose.yml)

```Dockerfile
FROM nginx:stable

EXPOSE 81
```

Modifier _docker-compose.yml_

```yaml
services:
  nginx:
    build: .
    ports:
      - 8080:81 # A gauche le port du HOST : à droite le port du CONTAINER
```

#### :bike: Turn up the volume

##### SANS VOLUME

:point_right: Reprenez le fichier Docker Compose du challenge précédent "Web compose" et démarrez le service "nginx".

N'oubliez pas de mettre les fichier de nginx.conf et index.html modifiés dans le dossier projet host

:point_right: Trouver un moyen d’exécuter l'interpréteur de commande bash dans le conteneur lié au service "nginx" via la commande ```docker compose```.

```bash
docker compose exec -it <NOM DU SERVICE DANS LE YAML> /bin/bash
```
> [!WARNING]
> Différent de docker exec -it \<ID ou NAME du CONTAINER\>

> [!TIP]
> En cas de problème, n'hésitez pas à RESET ALL 

```bash
docker compose down
# si permission denied: sudo aa-remove-unknown
docker container rm <ID CONTAINERS>
docker image rm <ID IMAGE>
docker system prune [--all]
sudo systemctl restart docker
```

👉 Une fois le terminal du conteneur disponible et attaché, exécutez la commande suivante afin de remplacer rapidement le contenu du fichier HTML utilisé par défaut par le serveur web.

```
echo "<p>This is a test</p>" > /usr/share/nginx/html/index-lacapsule.html
```

👉 Quittez le terminal interactif du conteneur et faites une requête vers le serveur web via curl afin de constater la modification.

👉 Arrêtez et supprimez le conteneur lié au service "nginx".

👉 Démarrez de nouveau le service nginx afin de refaire une requête vers le serveur web via curl.

Vous constatez que le fichier HTML originel est revenu, car ce qui se passe dans le conteneur est temporaire, il n’y a que ce qui est enregistré dans l’image qui sera conservé en cas de suppression du conteneur (du moins, pour le moment)

##### AVEC VOLUME

👉 Grâce à la documentation et la notion de volumes Docker, trouvez les instructions à ajouter dans le fichier Docker Compose afin que le dossier "/usr/share/nginx/html" soit monté (bind mount) sur la machine hôte.

_Ce dossier devra s’appeler "html" et sera automatiquement créé dans le même dossier que le fichier "docker-compose.yml" sur la machine hôte._

```yaml
services:
  nginx:
    build: .
    ports:
      - 8080:81
    volumes:
      - ./html:/usr/share/nginx/html
```

👉 Démarrez le service "nginx" et vérifiez que le dossier "html" a bien été créé sur la machine hôte.

👉 À l’intérieur de ce dossier "html", créez un fichier "index-lacapsule.html" avec le contenu de votre choix et redédmarrrez les services. Exécutez un curl pour vérifier que les modifs du index.html sont ok

```bash
curl http://localhost:8080
```

_Si le dossier a été créé automatiquement par Docker, il a très certainement les permissions root, il faudra donc modifier ses permissions **POUR L'ATTIBUER AU USER QUI RUN DOCKER COMPOSE**._