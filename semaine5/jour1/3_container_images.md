**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

**Semaine 5**

**Jour 1 : Conteneurisation**

---

# 3 - CONTAINER ET IMAGES

## <ins> Récupération d'une image </ins>

Une image Docker est un modèle en lecture seule, utilisée pour créer des conteneurs. Elle est composée de plusieurs couches empaquetant toutes les installations et dépendances nécessaires pour disposer d’un environnement de conteneur opérationnel.

👉 Listez les images disponibles sur le système.

docker images

Vous êtes censé voir l’image "hello-world" précédemment utilisée. Elle a été téléchargée automatiquement lors du lancement du conteneur, mais vous verrez qu’il est possible de récupérer une image sans lancer systématiquement un conteneur.

👉 À partir de la bibliothèque d’images Docker Hub, recherchez l’image officielle du système d’exploitation Debian et récupérez-la via la commande docker pull.

docker pull debian

👉 Vérifiez que l’image a bien été téléchargée via la commande docker images.

Vous pouvez voir que l’image "debian" dans sa version "latest" est beaucoup plus lourde, ce qui est logique, car il s’agit d’un système d’exploitation en version "light".

Pour information, si aucun tag n’est précisé, la version "latest" sera récupérée.

## <ins> Utilisation d'une image / container </ins>

👉 Levez un conteneur à partir de l’image "debian". Le conteneur devra porter le nom "cont-debian" plutôt qu’un nom auto-généré par Docker.
- docker run -d <detached> --name \<CONT NAME\> \<IMG NAME\>
```
docker run --name cont-debian debian
```

> [!WARNING]
> le container quitte immédiatement

👉 Supprimez le conteneur "cont-debian" et recréez le conteneur avec l’option -it afin de le lancer en mode interactif et le contrôler grâce à un terminal bash.
```
docker container rm cont-debian
docker run -it --name cont-debian debian
```

> [!INFO]
> vous arrivez dans la console du container

> [!WARNING]
> le container quitte quand vous quittez la console du : container 

- Pour garder le container ouvert et indépendant de la console HOST, il faut rajouter l'option -d \<DETACHED\> :
```
docker container rm cont-debian
docker run -it -d --name cont-debian debian
```
## <ins> Nettoyer le système </ins>

- arrêt des containers  
- suppression des containers
- suppression des images
- prune du système  
- restart du systeme (pour léibérer les ports nottement)
- 
```
docker stop <CONTAINER NAME / ID>
docker container rm <CONTAINER NAME / ID>
docker image rm <IMG NAME / ID>
docker system prune
sudo systemctl restart docker
```
