# Formation devOps

:pill: La capsule

:fire:  Documentation d'accompagnement au cycle devOps :fire:

---

## Semaine 4

### Jour 5 : Hackathon awesome pipelines

## 1. Initialisation du projet

Ici on nous demande d'initialser le projet dans 2 repository Gitlab :
- Le Frontend dans l'un
- Le Backend dans l'autre

### 1ere étape : Cloner les repos

On clone les repo du frontend et backend :
```bash
# Frontend
git clone http://192.168.2.28/hackathon2/frontend.git
# Backend
git clone http://192.168.2.28/hackathon2/backend.git
```

### 2eme étape : Supprimer le lien avec le dépôt distant original et hébergez le projet sur notre propre repo GitLab

On commence par frontend :
```bash
cd frontend
git remote remove origin
git remote add origin git@gitlab.com:imed92/frontend_lacapsule.git
git push 
``` 
Puis on fait pareil sur backend
```bash
cd ../backend
git remote remove origin
git remote add origin git@gitlab.com:imed92/backend_lacapsule.git
git push 
``` 
Maintenant on check si c'est bien push sur Gitlab

![](https://github.com/imed92/LaCapsule/blob/main/corrections/week4/day5/Frontendgitlab.png)

![](https://github.com/imed92/LaCapsule/blob/main/corrections/week4/day5/Backendgitlab.png)

Et voilà, c'est bien push sur nos repos distant

## 2. Configuration du projet
On va maintenant configurer notre projet
On rentre dans notre projet backend puis on liste nos branches

```bash
cd backend/
git branch
# On a que la branche main
* main
```

On a que la branche main, on va donc en créer 1 autre: preprod
```bash
git checkout -b prod
```
Puis on envoie cette branche sur le serveur distant
```bash
git push --set-upstream origin prod
```
On check via gitlab et :
![](./push_prod.png "Titre de l'image")

Une fois que c'est fait on rebascule sur main
```bash
git checkout -b main
```

On va maintenant se créer un serveur de base de données via le service MongoAtlas .
Voir ici comment faire :
Site de MongoAtlas : https://www.mongodb.com/atlas/database
Tuto comment créer sa bdd : https://drive.google.com/file/d/1fd8dN2LMvfxvjn8cqWoowVsz2wn7AZbs/view?usp%3Dsharing
Tuto remplir : https://drive.google.com/file/d/1QCH7Loa1tgZgErgFQWH3nFmHjAHtpmQN/view?usp%3Dsharing
Pour remplir sa base de données, il faut la remplir avec le contenu du fichier trips.json dans ce repo meme.

Pour mettre en place la connexion depuis MongoDB Compass, il faut renseigner l'url avec le password de son cluster MongoDB 
Ensuite, on créer la base de données nommé lacpasule, puis une collection qui sera dans ma bdd lacapsule. Cette collection sera nommée trips :
![](./mongopomapss.png "Titre de l'image")

Une fois la base de données et la collection trips créées, on importe le fichier json trips.json pour remplir notre collections trips avec les données du fichier trips.json.

![](./import_trips.png "Titre de l'image")
![](./importtrips.png "Titre de l'image")

Et voilà, trips.json a bien été importé dans notre collection trips.
Notre base de données lacapsule est bien hebergée sur un cluster et dans cette base de données on a maintenant une collection nommée trips avec ces données :

![](./donnees.png "Titre de l'image")

## 3. Tests Cypress

Familiarisez-vous avec les tests Cypress existants dans le backend et analysez le frontend pour créer quatre nouveaux tests :

Recherche d'un trajet Paris-Bruxelles pour la date du jour.

Test de la fonction de réservation.

Test de la suppression d'un élément du panier.

Test de la fonction d'achat.

Intégrez ces tests dans une pipeline d'intégration continue qui s'exécutera automatiquement en accord avec le GitLab flow.

Initialisez Node.js dans le frontend avec npm init -y pour utiliser le module http-server, nécessaire à l'exécution des tests Cypress.

## 4. Tests de montée en charge :

Utilisez l'outil Ddosify pour mettre en place des tests de montée en charge dans votre pipeline CI/CD, en cohérence avec le GitLab flow.

## 5. Déploiement continu :

Automatisez le déploiement du frontend sur Vercel avec la CLI et le backend aussi (Commencer par le backend). Pour exécuter des tests sur le frontend, déployez-le dans un environnement de test et intégrez cet environnement à votre flow en lui réservant une branche spécifique.

Bonus :

## Intégrez SonarQube pour analyser la qualité du code du frontend uniquement.

## Déployez le backend sur Northflank en utilisant la pipeline qu'ils proposent, après l'avoir d'abord déployé sur Vercel avec la CLI, comme pour le frontend.
