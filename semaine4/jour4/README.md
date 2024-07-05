# Formation devOps
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

## Semaine 4

### Jour 4 : Azure devOps ###

---

**1 - Azure devOps**

[ ] <ins>### Initialisation ###</ins>

[ ] <ins>### Gestion de l'agent ###</ins>

[ ] <ins>### Gestion de la pipeline ###</ins>

[ ] <ins>### Pipeline "classique" ###</ins>

**2 - ARTEFACTS EN OPTION**

[ ] <ins>### Commencer par les bases ###</ins>

[ ] <ins>### Enregistrer les artifacts ###</ins>

[ ] <ins>### Enregistrer les artifacts ###</ins>

**3 - MAKE IT WORK**



[ ] <ins>### Commencer par les bases ###</ins>


👉 Créez un nouveau projet nommé : “My Python Todos”.

👉 Accédez à l'onglet "Repos" et créez un nouveau repository Git vide.

👉 Clonez [ce repository](https://github.com/VipulKavar/To-do-App) sur votre ordinateur.

[Classique - voir les même étapes plus haut si galère]


👉 Envoyez le projet Python sur Azure DevOps.

> Comme le dernier step de <ins>Gestion de la pipeline</ins> ci-dessus




[ ] <ins>### Lier les WorkItems aux Commits ###</ins>


👉 Accédez à Azure Boards et créez les work items suivants.

    Un bug : “Déploiement de l’application non-fonctionnel”
    Une Tâche : “Changer le nom de l’application”

👉 Créez votre pipeline et committez-le en le liant au work item correspondant.

- Enable "lier work item et pipelines" : [Lier les Work Items aux Pipelines](https://learn.microsoft.com/en-us/azure/devops/pipelines/integrations/configure-pipelines-work-tracking?view=azure-devops)

- Créer azure-pipelines.yml à la racine du projet

```
trigger:
- main

pool:
 name: 'python-sample-pool'

steps:
  - script: echo "HellO World !"
```

- faire un git add et git commit -m "Message #\<ID DU WORK ITEM\>"

> Le link apparait dans le formulaire d'édition du Work Item


👉 Modifiez le nom de l’application et commitez les modifications en le liant au work item correspondant.



[ ] <ins>### Lier les WorkItems aux Commits ###</ins>

👉 Modifiez votre pipeline YAML pour ajouter des scripts ou des tâches qui mettent à jour automatiquement l'état des work items liés lorsque des événements spécifiques se produisent (lors du démarrage d'un build, d'un test réussi, ou d'un déploiement).

👉 Exécutez des tests et des déploiements pour valider que les work items sont correctement mis à jour à travers le processus de CI/CD.

👉 Assurez-vous que les états des work items reflètent avec précision les changements dans le code et les phases du pipeline.

<details>
    <summary>Script frankenstein.yml non testé</summary>

    trigger:
        branches:
            include:
            - '*'

            jobs:
            - job: Test
            steps:
            - script: echo "Starting test..."
                displayName: 'Starting test'
            
            - task: PowerShell@2
                inputs:
                targetType: 'inline'
                script: |
                    # Replace with your organization, project and token
                    $organization = "your-organization"
                    $project = "your-project"
                    $token = "$(System.AccessToken)"
                    $workItemId = "1" # Replace with your work item ID or dynamically fetch it
                    
                    # Update the work item
                    $uri = "https://dev.azure.com/$organization/$project/_apis/wit/workItems/$workItemId?api-version=6.0"
                    $headers = @{
                        "Content-Type" = "application/json-patch+json"
                        "Authorization" = "Bearer $token"
                    }
                    
                    $body = @"
                    [
                    {
                        "op": "add",
                        "path": "/fields/System.State",
                        "value": "In Progress"
                    }
                    ]
                    "@
                    
                    Invoke-RestMethod -Method Patch -Uri $uri -Headers $headers -Body $body
                displayName: 'Update work item to In Progress'
</details>
