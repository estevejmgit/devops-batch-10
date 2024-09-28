# Formation devOps

:pill: La capsule

:fire:  Documentation d'accompagnement au cycle devOps :fire:

---

## Semaine 5 :pager: 

Docker, Docker compose et Kubernetes pour faire tourner les containers !

### Jour 1 : Conteneurisation

#### :bike: Docker Begin

##### Installer Docker pour Debian 12

:fire: Firewall : Docker is only compatible with ```iptables-nft``` and ```iptables-legacy``` see the [Documentation](https://docs.docker.com/engine/install/debian/) if you plan to use one


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

## Nettoyer le système 

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
