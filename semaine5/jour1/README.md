# Formation devOps

:pill: La capsule

:fire:  Documentation d'accompagnement au cycle devOps :fire:

---

## Semaine 5 :pager: 

Docker, Docker compose et Kubernetes pour faire tourner les containers !

### Jour 1 : Conteneurisation

#### :bike: Docker Begin

##### Installer Docker pour Debian 12

See the [Documentation](https://docs.docker.com/engine/install/debian/)

:fire: Firewall : Docker is only compatible with ```iptables-nft``` and ```iptables-legacy``` if you plan to use one

:warning: si vous avez déjà des installations de docker, lisez bien [la doc](https://docs.docker.com/engine/install/debian/) pour les désinstaller !

#### :bike: Containers et Images

##### Récupération d'une image 

Une image Docker est un modèle en lecture seule, utilisée pour créer des conteneurs. Elle est composée de plusieurs couches empaquetant toutes les installations et dépendances nécessaires pour disposer d’un environnement de conteneur opérationnel.

:point_right: Utiliser l'image ```hello-world```.

```bash
docker pull hello-world # récupère l'image en local, sans lancer de container
docker images           # liste les images présentes localement
docker run hello-world  # lance le container, si l'image n'est pas en local, va la télécharger
```

Quand on a fait un ```docker run```, un container est créé à partir de l'image, un **NAME** et une **ID** lui sont assignés. On retrouve ces infos et d'autres avec la commande suivante :

```bash
docker ps -a  # liste tous les containers (même inactifs)
```

:informaton_source: les infos listées sont :

   - CONTAINER ID : Identifiant unique du conteneur
   - IMAGE : Image utilisée pour lever le conteneur (ici "hello-world" où son seul rôle sera d’afficher un message sur le terminal)
   - COMMAND : Commande exécutée dans le conteneur ("/hello" qui correspond à un script créé par l’équipe de Docker pour afficher le message que vous avez pu voir tout à l’heure)
   - CREATED : Sans grande surprise, le délai écoulé depuis la création du container
   - STATUS : Information très importante, l’état du container ("exited" car il a été levé, la commande a été exécutée, puis le conteneur a été quitté)
   - PORTS : La liste des ports exposés entre le conteneur et la machine hôte (aucun pour le moment, car ce n’est pas utile)
   - NAMES : Le nom unique de chaque container pour les manipuler plus facilement (il est auto généré par Docker ou spécifié lors de la commande docker run avec l’option --name)

:point_right: À partir de la bibliothèque d’images Docker Hub, recherchez l’image officielle du système d’exploitation Debian et récupérez-la via la commande docker pull.

```docker pull debian```

:point_right: Vérifiez que l’image a bien été téléchargée via la commande ```docker images```.

Vous pouvez voir que cette image "debian" dans sa version "latest" est beaucoup plus lourde, ce qui est logique, car il s’agit d’un système d’exploitation en version "light".

Pour information, si aucun tag n’est précisé, la version "latest" sera récupérée.

```bash
docker run debian:latest
```

##### Utilisation d'une image / container 

:point_right: Levez un conteneur à partir de l’image "debian". Le conteneur devra porter le nom "cont-debian" plutôt qu’un nom auto-généré par Docker.

- docker run --name \<CONT NAME\> \<IMG NAME\>

```bash
docker run --name cont-debian debian
```

> [!WARNING]
> le container quitte immédiatement après s'être lancé ...

:point_right: Supprimez le conteneur "cont-debian" et recréez le conteneur avec l’option -it afin de le lancer en mode interactif et le contrôler grâce à un terminal bash.

```
docker container rm cont-debian
docker run -it --name cont-debian debian
```

> [!INFO]
> vous arrivez dans la console du container  
> le container quitte quand vous quittez la console du : container 

:star: Pour garder le container ouvert et indépendant de la console HOST, il faut rajouter l'option -d \<DETACHED\> :

```
docker container rm cont-debian
docker run -it -d --name cont-debian debian
```

##### Nettoyer le système 

- arrêt des containers  
- suppression des containers
- suppression des images
- prune du système  
- restart du systeme (pour libérer les ports nottement)
  
```
docker stop <CONTAINER NAME / ID>
docker container rm <CONTAINER NAME / ID>
docker image rm <IMG NAME / ID>
docker system prune -a
sudo systemctl restart docker
```

```docker system prune``` : nettoie les objets inutilisés sauf les images non utilisées mais encore associées à des conteneurs.  
```docker system prune -a``` : nettoie tout, y compris les images non utilisées qui ne sont associées à aucun conteneur.

#### :bike: My Best Friend Nginx

##### Docker, nginx et ports 

:point_right: Levez un conteneur Docker nommé "cont-nginx" basé sur [l’image officielle de nginx](https://hub.docker.com/_/nginx) 
Attention, à l’inverse de l’image debian, vous devrez lever le conteneur en mode détaché (via l’option -d) afin qu’il puisse se démarrer en tâche de fond.

```
docker run -it -d --name cont-nginx nginx:latest
```

> A ce stade, le container est lancé mais n'est pas joingable car aucun ports n'a été spécifié

:point_right: Supprimez le conteneur précédemment créé et re-créez en un nouveau avec l’option -p en précisant le port que l’on souhaite "bind" sur la machine hôte ainsi que le port cible.

_docker run -d -p \<HOST_PORT\>:\<CONT_PORT\> --name \<GIVE_CONT_NAME\> \<IMG_NAME\>_

```
docker stop cont-nginx
docker container rm cont-nginx
docker run -d -p 8080:80 --name cont-nginx nginx
```

##### Les logs de nginx via docker 

:point_right: Dans la documentation des commandes Docker, trouvez la commande et l’option vous permettant de consulter les logs du conteneur en temps réel. Essayez de faire une nouvelle requête afin de voir si elle est affichée dans les logs.

```
docker logs -f cont-nginx
```

##### Modifier le container 

:point_right: Trouvez un moyen "d’entrer" dans le conteneur afin de modifier le contenu du fichier chargé d’afficher le message de bienvenue de Nginx pour le remplacer par votre propre message.

- Entrer dans le container :

```
docker exec -it cont-nginx /bin/bash
```

- Modifier le fichier html par détaut dans /usr/share

```
container$: echo "REPLACE NGINX DEFAULT HTML" > /usr/share/nginx/html/index.html
container$: exit             # on sort du container
curl http://localhost:8080   # on vérifie si la modif a été prise en compte
```

> [!WARNING]
> Ces modifs ne durent que le temps que le container soit up. si le container s'arrête, les modifs sont perdues

#### :bike: Dockerfile

#####  Création du Dockerfile 

:point_right: Faites le ménage !

```
docker stop <NOM CONTAINER>
docker container rm <NOM CONTAINER>
docker image rm <NOM IMG>
docker system prune -a
sudo systemctl restart docker
```

:point_right: Créez un fichier Dockerfile et insérez-y les instructions suivantes.

```
FROM nginx:latest

RUN touch /test.txt
```

Ce premier Dockerfile est assez simple pour commencer, car il se contente de reprendre l’image 
nginx dans sa dernière version (latest) et de créer un fichier "test.txt" à la racine du conteneur.

:point_right: À partir de la commande docker build et du Dockerfile, créez une image nommée "img-nginx".

```
docker build -t img-nginx .
```

:point_right: Vérifiez la création de votre image personnalisée via la commande ```docker images```.

##### Utilisation de l'image custom 

:point_right: Levez un container Docker nommé "cont-nginx" à partir de cette image "img-nginx".

```
docker run -d -p 8080:80 --name cont-nginx img-nginx
```

:point_right: Exécutez une requête vers le serveur web afin de constater qu’il est bien déployé.

```
curl http://localhost:8080
```
> Si vous récupérez une page HTML avec un message de bienvenue de Nginx, c’est que tout est opérationnel !

:point_right: Vérifiez si le fichier "test.txt" créé lors du build de l’image est bien présent à la racine du container.

```
docker exec -it cont-nginx /bin/bash
container$ ls -l
```

> ls -l depuis le container devrait vous afficher la racine du container Y COMPRIS le fichier test.txt

#### :bike: ADVANCED DOCKERFILE

:point_right: Grâce à un nouveau fichier Dockerfile, créez votre propre image Docker nommée "nginx-lacapsule" qui permettra de déployer un 
serveur web suivant les contraintes suivantes :

> Le serveur web Nginx sera utilisé en version stable (et non pas latest comme dans les challenges précédents)

> Le header de réponse ne devra pas afficher la version de Nginx (visible grâce à l’option -v de curl)

> Le port d’écoute de Nginx devra être remplacé par 81

> La page de bienvenue de Nginx sera remplacée par le fichier HTML fourni dans les ressources du challenge

- Créer sur le host un fichier **index.html** qui remplacera celui de nginx par défaut

```
echo "<h1>My Own HTML from host !</h1>" > index.html
```

- Toujours sur le host, créer le fichier de conf **nginx.conf** de nginx qu'on importera dans le container pour limiter l'afffichage de la version (_server_tokens off_) en écrasant le fichier de conf d'origine
  
```
##### Default server configuration

server {
        listen 80 default_server;
        listen [::]:80 default_server;
        server_name localhost;

        location / {
            root /usr/share/nginx/html;
            index index.html index.htm;
        }

        error_page 500 502 503 504   /50x.html;
        location = /50x.html {
            root /usr/share/nginx/html;
        }

        # http option
        server_tokens off;
}
```

- Enfin, encore sur le host, modifier le _Dockerfile_ :

```
FROM nginx:stable

EXPOSE 81

COPY ./index.html /usr/share/nginx/html/index.html

COPY ./nginx.conf /etc/nginx/conf.d/default.conf
```

:point_right: Une fois le Dockerfile prêt, créez l’image "nginx-lacapsule" qui devra être taguée avec "alpha" en guise de version (en plus de "latest" automatiquement)

```
docker build -t nginx-lacapsule:alpha .
```

:point_right: Vérifiez que chaque contrainte du challenge est respectée en démarrant un conteneur et en requêtant le serveur grâce aux commandes suivantes.

```
docker run -d -p 8080:81 --name cont-nginx nginx-lacapsule:alpha
curl -v http://localhost:8080
```
