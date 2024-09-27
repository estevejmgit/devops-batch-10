# :star: **TIPS & TRICKS** :star:

## CONSOLE COMMANDS


### Reload du shell après apt install

```bash
source ~/.bashrc
```

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

## SSH SECURITY

### SSH KEY GENERATION

- Pour une clef en ed_25519

```bash
ssh-keygen -t ed25519 -C "<user_name>"
```

- Pour une clef RSA (norme la plus répandue)

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```


### TEST CONNECTION PLATEFORME GIT

Test de connection au plateforme de répo git (exemple avec azure, valable avec gitlab et autre en remplaçant l'addresse de connection) :

```bash
ssh -T git@ssh.dev.azure.com # ou git@gitlab.com

> remote: Shell access is not supported.
> shell request failed on channel 0
```

si on obtiens ces deux messages ça veut dire que CA A MARCHE !!   malgré la formulation un peu obcure

## SHELL SCRIPT DELETE GITLAB REPO

```bash
#!/bin/bash

# Remove First Exit Instruction to run the script
echo "Remove First Exit Instruction to run the script"
exit 1

# Variables
GITLAB_URL="https://gitlab.com"  # Remplacer par l'URL de GitLab si c'est une instance auto-hébergée
PRIVATE_TOKEN="<YOUR_GIT_TOKEN>"

# Récupérer tous les projets
projects=$(curl --header "PRIVATE-TOKEN: $PRIVATE_TOKEN" "$GITLAB_URL/api/v4/projects?membership=true&per_page=100" | jq '.[] | {id: .id, name: .name}')

# Boucle pour chaque projet
for project in $(echo "$projects" | jq -r '. | @base64'); do
  _jq() {
    echo "${project}" | base64 --decode | jq -r "${1}"
  }

  project_name=$(_jq '.name')
  project_id=$(_jq '.id')

  # Demander si l'utilisateur veut supprimer le projet
  echo "Projet: $project_name (ID: $project_id)"
  read -p "Veux-tu supprimer ce projet ? (y/n) " confirm

  if [[ "$confirm" == "y" ]]; then
    echo "Suppression du projet: $project_name..."
    curl --request DELETE --header "PRIVATE-TOKEN: $PRIVATE_TOKEN" "$GITLAB_URL/api/v4/projects/$project_id"
    echo "Projet $project_name supprimé."
  else
    echo "Projet $project_name conservé."
  fi
done

echo "Opération terminée."
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
