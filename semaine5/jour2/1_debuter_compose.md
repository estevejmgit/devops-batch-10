**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

**Semaine 5 - Containers et orchestration**

**Jour 2 : Compose**

---

# 1 - Présentation compose

[ ] <ins> Découverte </ins>

👉 Installer [docker compose](https://docs.docker.com/engine/install/linux) 
(! Attention docker**-**compose s'installe avec le binaire)

👉 Créez un fichier "docker-compose.yml" censé créer un service (conteneur) lançant l’image "hello-world".  
~~L’instruction "version" permet de spécifier la version du fichier Docker Compose qu’on souhaite utiliser~~ (déprécié)

```
services:
  helloworld:
    image: "hello-world:latest"
```
> on peut le lancer avec <mark>docker compose up</mark> avec l'option <mark>-d</mark> pour _detached_

👉 Afin de vous entraîner à manipuler le fichier Docker Compose, ajoutez un second service nommé "helloworld2" et basé sur la même image que le premier service.

```
services:
  helloworld:
    image: "hello-world:latest"
  helloworld2:
    image: "hello-world:latest"
```
> pour lancer un seul servicce : <mark>docker compose up helloworld2</mark>
