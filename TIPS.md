# :toolbox: **TIPS & TRICKS** :toolbox:

## CONSOLE COMMANDS

### lister les processus qui utilisent un port spécifié

```bash
sudo lsof -i -P -n | grep <NUM PORT>
```

### pour chercher une chaine de caractere dans des fichiers de manière recursive

```bash
grep -ri --include \*.yml -e 'hello world' ./
```

- -ri : _pour récursif et case insensitive_
- --include \*.yml : _tous les fichiers finissant par .yml_
- -e 'hello world' : _'expression à chercher'_
- ./ : _Path/To/Scan_

### Afficher le nom du propriétaire d'un fichier

```bash
stat -c "%U" nom_du_fichier
```

- stat -c "%U" : Affiche uniquement le nom du propriétaire du fichier.
- nom_du_fichier : Le nom du fichier

### Trouver tous les fichiers par nom dans un path spécifique

Pour trouver tous les fichiers qui correspondent au modèle file*.env dans un chemin spécifique, tu peux utiliser la commande find avec les options appropriées. Voici comment faire :

```bash
find /chemin/spécifique -type f -name 'file*.env'
```

- find : La commande de base pour rechercher des fichiers.

- /chemin/spécifique : Remplace ceci par le chemin du répertoire où tu veux effectuer la recherche.

- -type f : Indique que tu recherches des fichiers (f pour file).

- -name 'file*.env' : Le modèle de nom de fichier que tu cherches. Ici, file*.env signifie que tu recherches des fichiers dont le nom commence par "file" et se termine par ".env", avec éventuellement n'importe quel texte entre les deux.

## SSH KEY PAIR GENERATION

```bash
ssh-keygen -t ed25519 -C "<user_name>"
```

## DOCKER ET DOCKER COMPOSE

### ACCES CONTAINER ET VERIF ENV VAR

Entrer dans le container depuis la console locale

```bash
docker exec -it <nom_ou_id_container> sh
```

Vérifier la varibale d'environnement sur la console container

```bash
printenv | grep ENV_VAR_NAME
```

### Nettoyer les composantes DOCKER

```bash
docker compose down
docker container rm <ID CONTAINERS>
docker image rm <ID IMAGE>
docker system prune [--all]
sudo systemctl restart docker
```
