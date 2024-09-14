# Formation devOps

:pill: La capsule

:fire:  Documentation d'accompagnement au cycle devOps :fire:

---

**Semaine 5**

**Jour 5 : DOCKERFILE START**

---

# DOCKERFILE

## Création du Dockerfile 

👉 Faire le ménage !
```
docker stop <NOM CONTAINER>
docker container rm <NOM CONTAINER>
docker image rm <NOM IMG>
docker system prune
sudo systemctl restart docker
```

👉 Créez un fichier Dockerfile et insérez-y les instructions suivantes.

```
FROM nginx:latest

RUN touch /test.txt
```
Ce premier Dockerfile est assez simple pour commencer, car il se contente de reprendre l’image 
nginx dans sa dernière version (latest) et de créer un fichier "test.txt" à la racine du conteneur.

👉 À partir de la commande docker build et du Dockerfile, créez une image nommée "img-nginx".

```
docker build -t img-nginx
```

👉 Vérifiez la création de votre image personnalisée via la commande docker images.

## Utilisation de l'image custom 

👉 Levez un container Docker nommé "cont-nginx" à partir de cette image "img-nginx".

```
docker run -d -p 8080:80 --name cont-nginx img-nginx
```

👉 Exécutez une requête vers le serveur web afin de constater qu’il est bien déployé.

```
curl http://localhost:8080
```
> Si vous récupérez une page HTML avec un message de bienvenue de Nginx, c’est que tout est opérationnel !

👉 Vérifiez si le fichier "test.txt" créé lors du build de l’image est bien présent à la racine du container.

```
docker exec -it cont-nginx /bin/bash
container$ ls -l
```

> ls -l depuis le container devrait vous afficher la racine du container Y COMPRIS le fichier test.txt
