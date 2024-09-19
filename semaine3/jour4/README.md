# Formation devOps

:pill: La capsule

:fire:  Documentation d'accompagnement au cycle devOps :fire:

---

## Semaine 3 :zap:

Versionning avancé avec Git, Jira et intégration continue et tests d'intégration

### Jour 4 : Framework de Test (Cypress)

Avant de passer aux Challenge, se renseigner sur le [HTML et les CSS selector](https://developer.mozilla.org/fr/docs/Learn/CSS/Building_blocks/Selectors)

:information_source: **En fonction de la taille de la fenêtre du navigateur, le HTML peut changer !! Les css selectors aussi ...**

- cy.get("input[type='search']").type("DevOps");  
le css selector c'est _input[type='search']_ 

#### :bike: Cypress begin

##### Installation de Cypress

:warning: !! Attention dans l'install node il ya deux commandes : NVM  et NPM !!

- NVM : Node Version Manager
- NPM : Node Package Manager 

:warning: Pour Cypress meets gitlab, si vous parvenez pas à lancer yarn start

il faut faire yarn outdated afin d'avoir les librairies à mettre à jour  
Puis changer les numéros de versions dans le fichier package.json  
Et refaire yarn install

_Après ces manips yarn start devrait fonctionner_

##### Visiter une page

:point_right: Créez un fichier "wikipedia.cy.js" dans le dossier "e2e" (depuis VS Code) et explorez la
[documentation de Cypress](https://docs.cypress.io/guides/end-to-end-testing/writing-your-first-end-to-end-test) pour construire un scénario qui simulera simplement la navigation vers la page d'accueil de Wikipédia.

```javascript
describe("Testing Wikipedia", () => {          // nom du job courant
    it("Search for content", () => {           // nom de l'étape du job
        cy.visit("https://fr.wikipedia.org/"); // action : visiter le site wikipedia
    });
});
```

##### Accéder à l'élément d'une page

le module Chrome "Testing Playground" n'est plus supporté par toutes les version de Chrome : il faudra peut-être faire sans !

##### Interagir avec les éléments

:point_right: Créez un nouveau fichier "switch_language.cy.js" et construisez un test qui simulera le
changement de langue sur la page d’accueil de wikipedia pour le polonais. Assurez-vous d’être
bien arrivé sur la page qui contiendra "Bienvenue sur Wikipedia" en polonais.
Notez qu’il faut parfois forcer l’attente via l’instruction **cy.wait()**.

```javascript
describe("Testing Wikipedia", () => {                           // nom du job courant
    it("Switch language", () => {                               // nom de l'étape du job
        cy.visit("https://fr.wikipedia.org/");                  // action : visiter wikipedia
        cy.get("#p-lang-btn-checkbox").click();                 // action get : réaliser une action javascript click sur
                                                                //              sur l'objet HTML dont l'id est p-lang-btn-checkbox
                                                                //              (c'est la liste des langues disponibles)
        cy.wait(3000);                                          // action wait : Attendre x milisecondes
        cy.contains("Polski").click();                          // action contains : vérifie la présence de l'option Polski et click
                                                                //                   (car on a ouvert le menu avec get ci-dessus)
        cy.url().should("contain", "https://pl.wikipedia.org/");// action url().should(contains, "contenu recherché")
                                                                //                  vérifie la conformité de l'url par rapport 
        cy.contains("Witaj w Wikipedii");                       // action contains : vérifie la présence du texte dans la page
    });
});
```

#### :bike: Cypress meets GitLab

##### Setup Cyprerss

:point_right: Arrêtez le projet (via Ctrl + C) puis supprimez la liaison entre le dépôt local et le dépôt
distant. Vous créerez une liaison avec un nouveau dépôt git que vous aurez ouvert sur gitlab

```bash
git remote rm origin
git remote add origin <ULR_NOUVEAU_DEPOT>
```

##### Création des tests

:point_right: Créez des tests simples (un “it” par test) qui s’assurent que les features principales de la todo app fonctionnent :

- Ajout d’une todo et affichage de celle-ci
- Compteur du nombre de todos
- Sélection d’une todo et actualisation automatique du compteur de todos sélectionnées



