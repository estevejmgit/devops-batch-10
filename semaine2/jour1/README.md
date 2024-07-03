# Formation devOps
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

## Semaine 2 - BDD, Réseaux, SSH, GIT

### Jour 1 : BDD ###

---

**1 - START WITH POSTGRESQL**


[ ] <ins>### Install ###</ins>


👉 Installez le serveur PostgreSQL à l’aide des 3 commandes suivantes.

```
sudo apt update
sudo apt install -y postgresql postgresql-contrib
```

Vérfier le cluster dans la liste et démarrer:

```
pg_lsclusters
```
> liste  avec NUM / NAME

```
sudo pg_ctlcluster <NUM> <NAME> start
```

👉 Vérifiez que votre serveur est bien installé et démarré en vous y connectant avec l’utilisateur "postgres" via sudo, puis affichez la version de PostgreSQL.

```
sudo -u postgres psql
```

```
postgres=# SELECT VERSION();
```


[ ] <ins>### Création d'un utilisateur local ###</ins>

👉 À l’installation, le super user par défaut est "postgres". Accédez au shell psql en tant que "postgres" et créez un nouvel utilisateur "developer" avec le mot de passe "qwerty".

```
postgres=# CREATE USER developer WITH ENCRYPTED PASSWORD 'qwerty';
```



[ ] <ins>### Création d'un utilisateur local et d'une DB ###</ins>

👉 Créez une base de données appelée "mydb".

```
CREATE DATABASE mydb;
```

👉 Attribuez tous les droits à l’utilisateur "developer" sur la base de données nouvellement créée.

```
GRANT ALL ON DATABASE mydb TO developer;
ALTER DATABASE mydb OWNER TO developer;
```

👉 Déconnectez vous de la base de données via le raccourci "Ctrl + D" puis connectez-vous à la base de données avec le nouvel utilisateur "developer"

```
psql -U developer -h 127.0.0.1 -d mydb
```

Contrairement à tout à l’heure, vous ne passez par sudo afin de vous connecter à la base de données, car vous n’utilisez plus l’utilisateur "postgres".

_- L’option "-U" permet de spécifier le nom de l’utilisateur avec lequel vous voulez vous connecter à la base de données_

_- L’option "-h" permet de forcer la connexion à la base de données local (d’où l’IP 127.0.0.1), c’est obligatoire pour les utilisateurs autres que "postgres"_

_- L’option "-d" permet de sélectionner la base de données "mydb"_



[ ] <ins>### Création d'une table ###</ins>

👉 Créez une nouvelle table "myusers" qui doit contenir les clés suivantes avec les types de données appropriés :
* id
* firstname
* lastname
* email
* role
* created_on
* last_login

```
mydb=> CREATE TABLE myusers(   
    id serial PRIMARY KEY,   
    firstname VARCHAR NOT NULL,   
    lastname VARCHAR NOT NULL,   
    email VARCHAR UNIQUE NOT NULL,   
    role VARCHAR NOT NULL,   
    created_on TIMESTAMP NOT NULL,   
    last_login TIMESTAMP 
);
```
