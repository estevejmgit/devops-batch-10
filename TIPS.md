🧰 **TIPS & TRICKS** 🧰



## CONSOLE COMMANDS

### lister les processus qui utilisent un port spécifié

```
sudo lsof -i -P -n | grep <NUM PORT>
```
### pour chercher une chaine de caractere dans des fichiers de manière recursive

_-ri pour récursif et case insensitive, tous les fichiers finissant par .yml, -e 'pour expression à chercher' Path/To/Scan

```
grep -ri --include \*.yml -e 'hello world' ./
```

### Afficher le nom du propriétaire d'un fichier

```bash
stat -c "%U" nom_du_fichier
```

Explication :

    stat -c "%U" : Affiche uniquement le nom du propriétaire du fichier.
    nom_du_fichier : Remplace ceci par le nom du fichier pour lequel tu veux connaître le propriétaire.

### Trouver tous les fichiers par nom dans un path spécifique

Pour trouver tous les fichiers qui correspondent au modèle file*.env dans un chemin spécifique, tu peux utiliser la commande find avec les options appropriées. Voici comment faire :

```bash
find /chemin/spécifique -type f -name 'file*.env'
```

Explication :

find : La commande de base pour rechercher des fichiers.
    
/chemin/spécifique : Remplace ceci par le chemin du répertoire où tu veux effectuer la recherche.
    
-type f : Indique que tu recherches des fichiers (f pour file).
    
-name 'file*.env' : Le modèle de nom de fichier que tu cherches. Ici, file*.env signifie que tu recherches des fichiers dont le nom commence par "file" et se termine par ".env", avec éventuellement n'importe quel texte entre les deux.

## SSH KEY PAIR GENERATION

```
ssh-keygen -t ed25519 -C "<user_name>"
```

## Docker et docker compose

### ACCES CONTAINER ET VERIF ENV VAR

Entrer dans le container depuis la console local$
```
docker exec -it <nom_ou_id_container> sh
```

Vérifier la varibale sur la console container#
```
printenv | grep ENV_VAR_NAME
```

### Nettoyer les composantes DOCKER

```
docker compose down
(si permission denied: sudo aa-remove-unknown)
docker container rm <ID CONTAINERS>
docker image rm <ID IMAGE>
docker system prune [--all]
sudo systemctl restart docker
```

### En cas de docker compose down : permission denied

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
## GIT 

### Git divergent Branches

_Attention : si des modifs disatntes et locales n'ont pas été synchronisées, le distant peut prendre le pas sur le local_

```
git fetch origin
git rebase origin/main
```



