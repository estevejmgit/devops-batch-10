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
