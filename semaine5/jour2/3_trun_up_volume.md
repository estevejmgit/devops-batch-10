**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

**Semaine 5 - Containers et orchestration**

**Jour 2 : Compose**

---

# 3 - Turn up the volume

👉 Reprenez le fichier Docker Compose du challenge précédent "Web compose" et démarrez le service "nginx".

N'oubliez pas de mettre les fichier de nginx.conf et index.html modifiés dans le dossier projet host

👉 Trouver un moyen d’exécuter l'interpréteur de commande bash dans le conteneur lié au service "nginx" via la commande docker-compose.

```
docker compose exec -it <NOM DU SERVICE DANS LE YAML> /bin/bash
```
> [!WARNING]
> Différent de docker exec -it \<ID ou NAME du CONTAINER\>

> [!TIP]
> En cas de problème, n'hésitez pas à RESET ALL :
```
docker compose down
(si permission denied: sudo aa-remove-unknown)
docker container rm <ID CONTAINERS>
docker image rm <ID IMAGE>
docker system prune
sudo systemctl restart docker
```

👉 Une fois le terminal du conteneur disponible et attaché, exécutez la commande suivante afin de remplacer rapidement le contenu du fichier HTML utilisé par défaut par le serveur web.

```
echo "<p>This is a test</p>" > /usr/share/nginx/html/index-lacapsule.html
```

👉 Quittez le terminal interactif du conteneur et faites une requête vers le serveur web via curl afin de constater la modification.

👉 Arrêtez et supprimez le conteneur lié au service "nginx".

👉 Démarrez de nouveau le service nginx afin de refaire une requête vers le serveur web via curl.

Vous constatez que le fichier HTML originel est revenu, car ce qui se passe dans le conteneur est temporaire, il n’y a que ce qui est enregistré dans l’image qui sera conservé en cas de suppression du conteneur (du moins, pour le moment)
