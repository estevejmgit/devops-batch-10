# Formation devOps

:pill: La capsule

:fire:  Documentation d'accompagnement au cycle devOps :fire:

---

**Semaine 5 - Containers et orchestration**

**Jour 2 : Compose**

---

# 4 - ENV VARIABLES

## 1 - Les Variables d'environnement

Vous avez pu brièvement vous confronter au principe d’environnement précédemment dans la formation, notamment dans 
le challenge "Database deployment".

```
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

👉 Afin de découvrir le fonctionnement des variables d’environnement, démarrez le service "database" décrit dans le fichier Docker Compose ci-dessus et exécutez un terminal bash à l’intérieur du conteneur.

```
docker compose up -d 
docker compose exec -it database /bin/bash
```

👉 Exécutez la commande env afin de constater que la variable d’environnement précisée dans le fichier Docker Compose apparaît. Cette dernière sera exploitée par le service de PostgreSQL.

```
env
```
Sortie attendue :
> HOSTNAME=\<ID CONTAINER\>  
> PSOTGRES_PASSWORD=acknowledge_me  
> [...]

## 2 - Avec Docker

👉 Créez un fichier Dockerfile afin de construire une image nommée "mymails" basée sur debian (dans sa dernière version).

Cette image se contentera de récupérer une variable d’environnement nommée "EMAIL" qui aura "admin@test.com" comme valeur par défaut afin de 
l’afficher via la commande echo.

_Dans un Dockerfile, l’instruction "ENV" permet de préciser une variable d’environnement par défaut tandis que "CMD" 
permet d’exécuter une commande au lancement du conteneur._

```
FROM debian:latest

ENV EMAIL=admin@test.com

CMD echo ${EMAIL}
```

👉 Buildez l’image "img-debian-mail" associée à ce Dockerfile afin de pouvoir l’utiliser dans un fichier Docker Compose.

```
docker build -t img-debian-mail .
```

👉 Créez un nouveau fichier _docker-compose.yml_ contenant un service "mymails" basé sur l’image précédemment buildée.

```
services:
  mymails:
    build: .
```

👉 Démarrez le service "mymails" en mode attaché (sans l’option -d) afin de vérifier si l’email précisé dans le Dockerfile est bien affiché.

```
docker compose up
```

> mymails-1  | admin@test.com

## 3 - Avec docker compose

👉 Trouvez un moyen d’écraser la variable d’environnement "EMAIL" directement à partir du fichier Docker Compose
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


## Avec les ENV FILE

👉 Grâce à la documentation, trouvez un moyen de définir une variable d’environnement dans le fichier Docker Compose, mais en précisant sa valeur dans un fichier à part nommé "my.env", dans le même dossier.


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
> en gros, les **ENV VAR** du _Dockerfile_ sont écrasées par les **env_file** appelé dans le _docker-compose.yml_,
> et sont écrasée encore si elles sont re-dédfinie dans ce même docker-compose.yml avecl'instruction **environment:** (commenté dans l'exemple ci-dessus)




