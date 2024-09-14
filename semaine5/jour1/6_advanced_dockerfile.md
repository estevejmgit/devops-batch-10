# Formation devOps

:pill: La capsule

:fire:  Documentation d'accompagnement au cycle devOps :fire:

---

**Semaine 5**

**Jour 1 : Conteneurisation**

---

# 6 - ADVANCED DOCKERFILE

👉 Grâce à un nouveau fichier Dockerfile, créez votre propre image Docker nommée "nginx-lacapsule" qui permettra de déployer un 
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
# Default server configuration
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

👉 Une fois le Dockerfile prêt, créez l’image "nginx-lacapsule" qui devra être taguée avec "alpha" en guise de version (en plus de "latest" automatiquement)

```
docker build -t nginx-lacapsule:alpha .
```

👉 Vérifiez que chaque contrainte du challenge est respectée en démarrant un conteneur et en requêtant le serveur grâce aux commandes suivantes.

```
docker run -d -p 8080:81 --name cont-nginx nginx-lacapsule:alpha
curl -v http://localhost:8080
```
