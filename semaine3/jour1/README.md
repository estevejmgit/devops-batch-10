# Formation devOps

:pill: La capsule

:fire:  Documentation d'accompagnement au cycle devOps :fire:

---

## Semaine 3 :zap:

Versionning avancé avec Git, Jira et intégration continue et tests d'intégration

### Jour 1 : Git Avancé

#### :bike: Branch Theft Auto

:warning: Il faut parfois recharger [l'interface web de visualisation des branches](https://onlywei.github.io/explain-git-with-d3/) quand on a une visualisation incohérente

##### Découverte des branches

##### Initialisation d’un repository

##### Création d’une branche

##### Gestion de conflits

##### Visualisation des branches

#### :bike: GitLab basics

##### Créer un repository sur GitLab

##### Se connecter à un dépôt distant

##### Envoyer des modifications

##### Récupérer les modifications

#### :bike: GitLab flow

##### Authentification par clé SSH

##### Création d’un groupe sur GitLab

##### Création d’un ticket sur GitLab

##### Gitlab Flow

##### Cloner la codebase en local

##### Création d’une merge request

##### Merge de main dans production

##### Finalisez votre première release

#### :bike: GitLab combat

##### Conflits avec Git

#### :bike: Auto Git

##### README Templating (Create distant repo from local)

##### Bash scripting

- script to delete repo distant

```bash
#!/bin/bash

# Remove First Exit Instruction to run the script
echo "Remove First Exit Instruction to run the script"
exit 1

# Variables
GITLAB_URL="https://gitlab.com"  # Remplacer par l'URL de GitLab si c'est une instance auto-hébergée
PRIVATE_TOKEN="glpat-KTQxWhsaHzAzDUf3aB_c"

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
