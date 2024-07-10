**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

**Semaine 5 - Containers et orchestration**

**Jour 2 : Compose**

---

# 5 - DATABASE DEPLOY WITH DOCKER

## 1 - Déployer une DB

👉 Sur le hub d’images Docker, trouvez l’image adaptée afin de déployer une base de données PostgreSQL.

👉 Créez un nouveau fichier Docker Compose contenant un service nommé "database" et  basé sur l’image précédemment trouvée.

Le service devra être configuré pour respecter ces deux contraintes :

- Le mot de passe de l’utilisateur créé par défaut sera "acknowledge_me"
- Même si le conteneur lié au service est supprimé, les données devront être persistantes grâce à un [volume](https://docs.docker.com/storage/volumes/) créé et managé par Docker. Ce volume nommé "db_data" devra être créé et utilisé dans le fichier Docker Compose.


```
services:
  database:
    image: postgres:latest
    container_name: postgres_container
    environment:
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: acknowledge_me
      POSTGRES_DB: your_database
    ports:
      - "5432:5432"
    volumes:
      - db_data:/var/lib/postgresql/data

volumes:
  db_data:
```
