# 🧰 TIPS & TRICKS 🧰

- lister les processus qui utilisent un port :

```
sudo lsof -i -P -n | grep <NUM PORT>
```


- Nettoyer les composantes DOCKER

```
docker stop <CONTAINER NAME / ID>
docker container rm <CONTAINER NAME / ID>
docker image rm <IMG NAME / ID>
docker system prune
sudo systemctl restart docker
```
