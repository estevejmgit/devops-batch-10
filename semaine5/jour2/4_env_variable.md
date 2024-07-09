**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

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
