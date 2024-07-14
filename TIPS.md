# 🧰 TIPS & TRICKS 🧰

**lister les processus qui utilisent un port**

```
sudo lsof -i -P -n | grep <NUM PORT>
```


**Nettoyer les composantes DOCKER**

```
docker compose down
(si permission denied: sudo aa-remove-unknown)
docker container rm <ID CONTAINERS>
docker image rm <ID IMAGE>
docker system prune [--all]
sudo systemctl restart docker
```

**En cas de docker compose down : permission denied**

```
sudo aa-remove-unknown
```
_si apparmor est demandé pour le restart_
start the appormor system
```
sudo systemctl start apparmor 
```
parse and reload all apparmor profiles of installed snap applications 
```
sudo apparmor_parser -r /var/lib/snapd/apparmor/profiles/*
```

**Git divergent Branches**

_si des modifs disatntes et locales n'ont pas été synchronisées_

```
git fetch origin
git rebase origin/main
```

**pour chercher une chaine de caractere dans des fichiers de manière recursive**

_-ri pour récursif et case insensitive, tous les fichiers finissant par .yml, -e 'pour expression à chercher' Path/To/Scan

```
grep -ri --include \*.yml -e 'hello world' ./
```

