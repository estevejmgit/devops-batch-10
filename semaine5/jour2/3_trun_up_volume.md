**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

**Semaine 5 - Containers et orchestration**

**Jour 2 : Compose**

---

# 3 - Turn up the volume

👉 Reprenez le fichier Docker Compose du challenge précédent "Web compose" et démarrez le service "nginx".

👉 Trouver un moyen d’exécuter l'interpréteur de commande bash dans le conteneur lié au service "nginx" via la commande docker-compose.

```
docker compose exec -it <NOM DU SERVICE DANS LE YAML> /bin/bash
```

> [!WARNING]
> Différent de docker exec -it \<ID ou NAME du CONTAINER\>



