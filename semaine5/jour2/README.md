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

:point_right: Pour supprimer les containers

```bash
docker compose down
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
docker compose up -d
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
> En cas de problèmes, n'hésitez pas à RESET ALL et à recommencer 


:point_right: Une fois le terminal du conteneur disponible et attaché, exécutez la commande suivante afin de remplacer rapidement le contenu du fichier HTML utilisé par défaut par le serveur web.

```bash
container$: echo "<p>This is a test</p>" > /usr/share/nginx/html/index-lacapsule.html
```

:point_right: Quittez le terminal interactif du conteneur et faites une requête vers le serveur web via curl afin de constater la modification.

:point_right: Arrêtez et supprimez le conteneur lié au service "nginx".

:point_right: Démarrez de nouveau le service nginx afin de refaire une requête vers le serveur web via curl.

Vous constatez que le fichier HTML originel est revenu, car ce qui se passe dans le conteneur est temporaire, il n’y a que ce qui est enregistré dans l’image qui sera conservé en cas de suppression du conteneur (du moins, pour le moment)

##### AVEC VOLUME

:point_right: Grâce à la documentation et la notion de volumes Docker, trouvez les instructions à ajouter dans le fichier Docker Compose afin que le dossier "/usr/share/nginx/html" soit monté (bind mount) sur la machine hôte.

_Ce dossier devra s’appeler "html" et sera automatiquement créé dans le même dossier que le fichier "docker-compose.yml" sur la machine hôte._

```yaml
services:
  nginx:
    build: .
    ports:
      - 8080:81
    volumes:
      - ./html:/usr/share/nginx/html    # à gauche le dossier HOST ':' à droite le dossier CONTAINER
```

:point_right: Démarrez le service "nginx" et vérifiez que le dossier "html" a bien été créé sur la machine hôte.

:point_right: À l’intérieur de ce dossier "html", créez un fichier "index-lacapsule.html" avec le contenu de votre choix et redédmarrrez les services. Exécutez un curl pour vérifier que les modifs du index.html sont ok

```bash
curl http://localhost:8080
```

#### :bike:  VARIABLES D'ENVIRONNEMENT

##### Définition des Variables d'environnement

Vous avez pu brièvement vous confronter au principe d’environnement précédemment dans la formation, notamment dans 
le challenge "Database deployment".

```yaml
services:
  database:
    image: "postgres:latest"
    ports:
      - "5432:5432"
    volumes:
      - ./db_data:/var/lib/postgresql/data
    environment:
      POSTGRES_PASSWORD: acknowledge_me
```

Si vous analysez ce fichier Docker Compose, vous pouvez voir qu’une variable d’environnement est spécifiée 
au lancement du conteneur : "POSTGRES_PASSWORD" qui aura pour valeur "acknowledge_me".

:point_right: Afin de découvrir le fonctionnement des variables d’environnement, démarrez le service "database" décrit dans le fichier Docker Compose ci-dessus et exécutez un terminal bash à l’intérieur du conteneur.

```
docker compose up -d 
docker compose exec -it database /bin/bash
```

:point_right: Exécutez la commande env afin de constater que la variable d’environnement précisée dans le fichier Docker Compose apparaît. Cette dernière sera exploitée par le service de PostgreSQL.

```
env
```
Sortie attendue :
> HOSTNAME=\<ID CONTAINER\>  
> PSOTGRES_PASSWORD=acknowledge_me  
> [...]

##### Avec Docker tout seul

:point_right: Créez un fichier Dockerfile afin de construire une image nommée "mymails" basée sur debian (dans sa dernière version).

Cette image se contentera de récupérer une variable d’environnement nommée "EMAIL" qui aura "admin@test.com" comme valeur par défaut afin de 
l’afficher via la commande echo.

_Dans un Dockerfile, l’instruction "ENV" permet de préciser une variable d’environnement tandis que "CMD" 
permet d’exécuter une commande au lancement du conteneur._

```Dockerfile
FROM debian:latest

ENV EMAIL=admin@test.com

CMD echo ${EMAIL}
```

:point_right: Buildez l’image "img-debian-mail" associée à ce Dockerfile afin de pouvoir l’utiliser dans un fichier Docker Compose.

```bash
docker build -t img-debian-mail .
```

:point_right: Créez un nouveau fichier _docker-compose.yml_ contenant un service "mymails" basé sur l’image précédemment buildée.

```
services:
  mymails:
    build: .
```

:point_right: Démarrez le service "mymails" en mode attaché (sans l’option -d) afin de vérifier si l’email précisé dans le Dockerfile est bien affiché.

```
docker compose up
```

> mymails-1  | admin@test.com

##### Avec docker compose

:point_right: Trouvez un moyen d’écraser la variable d’environnement "EMAIL" directement à partir du fichier Docker Compose
et démarrez le service afin de vérifier si l’email a bien été changé.

_docker-compse.yml_ :

```
services:
  mymails:
    build: .
    environment:
      - EMAIL=anewmail@test.com
```


```
docker compose up
```
> mymails-1  | anewmail@test.com


##### Avec Docker Compose et les .env

:point_right: Grâce à la documentation, trouvez un moyen de définir une variable d’environnement dans le fichier Docker Compose, mais en précisant sa valeur dans un fichier à part nommé "my.env", dans le même dossier.


_my.env_ :

```
EMAIL=a_brand_new_mail@test.com
```

_docker-compse.yml_ :

```
services:
  mymails:
    build: .
    # environment:
    #  - EMAIL=anewmail@test.com
    env_file: "my.env"
```
 

👉 Démarrez tous les services en spécifiant le fichier d’environnement "my.env" afin de vérifier que l’email soit bien affiché.

> [!WARNING]
> Prévalence des variables 'environment' dans _docker-compose.yml_ sur _env_file_ , qui lui-même prévaut sur le _Dockerfile_  
> les **ENV VAR** du _Dockerfile_ sont écrasées par les **env_file** appelé dans le _docker-compose.yml_,
> et sont écrasée encore si elles sont re-dédfinie dans ce même docker-compose.yml avecl'instruction **environment:** (commenté dans l'exemple ci-dessus)

#### :bike: DATABASE DEPLOY WITH DOCKER

##### Déployer une DB

👉 Sur le hub d’images Docker, trouvez l’image adaptée afin de déployer une base de données PostgreSQL.

👉 Créez un nouveau fichier Docker Compose contenant un service nommé "database" et  basé sur l’image précédemment trouvée.

Le service devra être configuré pour respecter ces deux contraintes :

- Le mot de passe de l’utilisateur créé par défaut sera "acknowledge_me"

- Même si le conteneur lié au service est supprimé, les données devront être persistantes grâce à un [volume](https://docs.docker.com/storage/volumes/) créé et managé par Docker. Ce volume nommé "db_data" devra être créé et utilisé dans le fichier Docker Compose.

👉 Modifiez le service "database" afin de "binder" le port par défaut de PostgreSQL sur la machine hôte.

```yaml
services:
  database:
    image: postgres:latest
    container_name: postgres_container
    environment:
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: acknowledge_me
      POSTGRES_DB: your_database
    ports:
      - "5432:5432" # à gauche le port du HOST : à droite le port du CONTAINER
    volumes:
      - db_data:/var/lib/postgresql/data # à gauche le volume du HOST : à droite le dossier du CONTAINER

volumes:
  db_data: # ! au ':' après le nom du volume !
```

:information_source: Dans l'exemple de déclaration de volume ci-dessus, le volume _db_data_ sera en bindé par Docker sur le HOST dans un PATH de type : ```/var/lib/docker/volumes/db_data/```.

On pourrait spécifier un chemin absolu en lieu et place de _db_data_ en mettant à gauche des ```:``` un **absolute path** comme ```/home/user/project/host_voume``` ou un **relative_path** comme ```./from/current/path```. Ces volumes ne seront PAS supprimé lors de l'usage du flag ```-v``` décrit ci-dessous.

:information_source: Pour supprimer les containers ET les volumes docker compose, on utilise le flag ```-v```

```bash
docker compose down -v
```