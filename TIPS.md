# 🧰 TIPS & TRICKS 🧰

- lister les processus qui utilisent un port :

```
sudo lsof -i -P -n | grep <NUM PORT>
```


- Nettoyer les composantes DOCKER

```
docker compose down
(si permission denied: sudo aa-remove-unknown)
docker container rm <ID CONTAINERS>
docker image rm <ID IMAGE>
docker system prune [--all]
sudo systemctl restart docker
```
