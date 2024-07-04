# Formation devOps
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

## Semaine 4

### Jour 4 : Azure devOps ###

---

**1 - Azure devOps**



[ ] <ins>### Initialisation ###</ins>

> Azure interface

> Connectez-vous à Azure DevOps, créez un compte puis une organisation 

> https://aex.dev.azure.com/me

> Créez un nouveau projet nommé : “My Flask App”.

> Accédez à l'onglet "Repos" et créez un nouveau repository Git vide.


👉 Clonez ce [repository](https://github.com/Microsoft/python-sample-vscode-flask-tutorial) sur votre ordinateur.

```
git clone https://github.com/Microsoft/python-sample-vscode-flask-tutorial
cd python-sample-vscode-flask-tutorial
```

👉 Changez origin pour l'url du repo fournie par azure

```
git remote rm origin
git remote add origin <url_repo_azure>
```

>  Azure Interface
>
> Créer les Git credentials ...
>
> user esteve.jm
> mdp zqsqyefvdufhleu5nnj2my3yg4243oe5dihcerb555jsctdz3tgq
>

👉 ... ou Mettez la connection SSH en place

```
ssh-keygen -t rsa-sha2-256 -b 2048
```

Laissez les options par défaut / **PAS DE PASSPHRASE**

```
cat ~/.ssh/id_rsa.pub
```

> Copier la clef et la rajouter sur le site de azureDevops


👉 Envoyez le projet python-sample-vscode-flask-tutorial sur Azure DevOps.

```
git add .
git commit -m "1er commit"
git push origin main
```



[ ] <ins>### Gestion de l'agent ###</ins>


👉 Téléchargez l’agent Azure DevOps sur votre VM. Désarchivez le fichier .tar.gz et lancez la configuration de l’agent.

> Créer un pool d'agent
>
_Interface Organisation sur AzureDevOps :_
- Tout en bas à gauche Organisation Settings
- Menu Gauche Pipelines > Agent Pools : Créer un nouveau Pool
- Onglet Agent : Bouton New Agent
- Récupérer l'url de l'agent
>

👉 En local :

```
mkdir ~/azureAgent && cd ~/azureAgent
wget \<URL DE L'AGENT\>
tar zxvf <NOM AGENT>.tar.gz # ex sur Linux à ce jour : vsts-agent-linux-x64-3.241.0.tar.gz
rm -f <NOM AGENT>.tar.gz
```

Configurez l'agent 

```
./config.sh
```

! Attention il demande en Français mais il faut Répondre en anglais

```
Accepter contrat licence ? > Y
URL serveur ? > https://dev.azure.com/{your-organization}
Type authentification > PAT
```

> NB : pour créer un personnal token : site azure > user setting (en haut à droite) > Personnal Access Token

```
Personnal Token > ************************************
Entrez pool d'agents (appuyez sur Entrée pour default) > <NOM POOL AGENT CREER CI-DESSUS>
Entrez nom de l’agent (appuyez sur Entrée pour <DEFAULT USER>) >  <VOTRE CHOIX>
Entrez dossierr de travail (default _work) > <LAISSER VIDE POUR DEFAUT>
```

👉 Installer l'agent en tant que service Système **systemd** (on pourra utiliser systemctl start agent)

```
sudo ./svc.sh install <LOCAL USER NAME>
```

Démarrer l'agent, check son status et l'arrêter pour tester, puis le lancer et le laisser tourner

```
sudo ./svc.sh start
sudo ./svc.sh status
sudo ./svc.sh stop
sudo ./svc.sh start
```



[ ] <ins>### Gestion de la pipeline ###</ins>

👉 Créez un fichier azure-pipelines.yml à la racine de votre projet.

👉 Configurez votre pipeline en utilisant votre agent local afin d’effectuer les actions suivantes 

- Copier les fichiers du projet vers le répertoire ~/myFlaskApp
- **<mark>Lancer le projet sur votre VM (????)</mark>** (voir ci-dessous)


NB : En fait il s'agit dans un 1er temps de set le .yml, de le push sur azuere et depuis azure de créer la pipeline et de run l'agent 

```
trigger:
- main

pool:
 name: 'python-sample-pool'

steps:
- script: cp -r ~/azureDevOps/python-sample-vscode-flask-tutorial/* ~/myFlaskApp
```

Pusher le repo 

```
git add .
git commit -m "ajout azure-pipelines.yml"
git push origin main
```

> Sur Azure Interface

> Menu Gauche > Pipelines > Create Pipeline
> Selectionner repo GIT > choisir le repo créer précédement
> valider le yaml
> cliquer sur run

> Vérifier le report du Job

> [!WARNING]

<mark>Lancer le projet sur votre VM (????)</mark>


<details>
    <summary>
        Exemple de pipeline.yml pour faire tourner le site
    </summary>
    ```
    trigger:
    - main

    pool:
    name: 'Default' 

    jobs:
    - job: BuildAndDeploy
    displayName: 'Build and Deploy Flask App'
    pool:
        name: 'Default' 

    steps:
    - script: |
        echo "Python version:"
        python3 --version
        echo "Installing dependencies"
        python3 -m venv venv
        source venv/bin/activate
        pip install -r requirements.txt
        displayName: 'Install dependencies'

    - script: |
        echo "Copying files to target directory"
        mkdir -p ~/myFlaskApp
        cp -r * ~/myFlaskApp
        displayName: 'Copy files to target directory'

    - script: |
        echo "Launching Flask app"
        cd ~/myFlaskApp
        source venv/bin/activate
        nohup ./venv/bin/python run.py
        displayName: 'Launch Flask app'
    ```

</details>




[ ] <ins>### Pipeline "classique" ###</ins>

👉 Créez un nouveau projet “My Classic Flask App” (sur azure) et importer le repo github fourni plus haut

👉 Activez les pipelines classiques au niveau de votre organisation. (settings de l'orga > pipelines > option à décocher)

👉 _Créez un pipeline en utilisant l’éditeur graphique de pipeline afin qu’il utilise votre agent local et qu’il effectue les mêmes actions que le pipeline précédent. (???)_


---

**2 - ARTEFACTS EN OPTION**



[ ] <ins>### Commencer par les bases ###</ins>

👉 Créez un nouveau projet nommé : “Weather Forecast”.

👉 Accédez à l'onglet "Repos" et créez un nouveau repository Git vide.

👉 Clonez ce [repository github](https://github.com/Adedoyin-Emmanuel/react-weather-app) sur votre ordinateur.

>NB : changer git remote rm origin / git remote add origin <git@REPO CREE CI-DESSUS>

👉 Envoyez le projet React sur Azure DevOps.

> _Alternativement on peut importer directement sur Azure le repo github et le cloner en local depuis azure (Attention au default branch name)_




[ ] <ins>### Enregistrer les artifacts ###</ins>

👉 Créez un fichier azure-pipelines.yml dans la racine de votre projet ReactJS.

👉 Configurez le pipeline pour installer les dépendances, packager les node_modules et les enregistrer comme artefacts.

NB : il faut faire un npm install puis regarder dans la doc azure publish artifacts :

```
trigger:
- master

pool:
 name: 'python-sample-pool'

steps:
- script: npm install 
# - script: tar -czf node_modules.tar.gz node_modules

- task: PublishPipelineArtifact@1
  inputs:
    # targetPath: '$(Pipeline.Workspace)'
    targetPath: 'node_modules'
    publishLocation: 'pipeline'
    artifact: 'drop'
```




[ ] <ins>### Enregistrer les artifacts ###</ins>


👉 Ajoutez une étape dans le pipeline pour <mark>déployer l'application</mark> ReactJS sur votre VM en utilisant les artefacts générés.


> [!TIP]
> Pour utiliser les Artefacts ajouter :
```
steps:
- download: current
  artifact: drop
  patterns: |
    **/*.js
```

> Pour déployer l'aPP, voire ci-dessus <mark>Lancer le projet sur votre VM (????)</mark>

---

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