# Formation devOps

:pill: La capsule

:fire:  Documentation d'accompagnement au cycle devOps :fire:

---

## Semaine 4 :tanabata_tree: 

Déploiement continu, tests de déploiement, Provider Cloud Azure DevOps


### Jour 5 : Hackathon Awesome Pipelines


Pour info, faites attention à plusieurs choses dans la connection DB :

    dans votre URL de connection, le user et mot de passe n'est pas le login /mdp du site mongoAtlas mais bien le user/mdp de l'utilisateur déclaré pour la Database !

    il est possible que l'URL de connection proposée sur le site de MongoAtlas soit incomplète, si vous avez un pb de connection entre votre backend et votre mongoDB, essayez de modifier la CONNECTION_STRING en rajoutant le nom de votre DATABASE avant le "?" : 

CONNECTION_STRING=mongodb+srv://[DB_USER]:[DB_USER_PASSWD]@[URL_DONNEE_PAR_MONGO_ATLAS]/[**NOM_DE_VOTRE_DB**]?retryWrites=true 

(remplacez les données entre [ ] par vos informations)