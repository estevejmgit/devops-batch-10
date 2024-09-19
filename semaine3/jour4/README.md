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

:warning:  Vérifier les dernières versions des package qu'on installe (depuis la publication du cours elles ont sans doute changé)

:warning: !! Attention dans l'install node il ya deux commandes : NVM  et NPM !!

- NVM : Node Version Manager
- NPM : Node Package Manager 

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


```javascript
describe("Testing Todo App", () => {        // nom du job
    beforeEach(() => {                      // Avant chaque étape du job
        cy.visit("http://localhost:3000");  // on visite le site en local
    });

    it("Add todos", () => {                                         // étape ajout d'éléments dans la liste
        cy.contains("Click here to login").click();                 // Click sur l'élément HTML qui contient "Click here to login"
        cy.get("#title").type("Faire les courses").type("{enter}"); // Dans l'élément HTML dont l'id est title, on écrit "Faire les courses"
                                                                    // et on simule un press sur la touche ENTER du clavier
        cy.get("#title").type("Ranger les courses").type("{enter}");//  Dans l'élément HTML dont l'id est title, on écrit "Ranger les courses"
                                                                    // et on simule un press sur la touche ENTER du clavier
        cy.contains("Faire les courses");                           // on vérifie que la page contient bien Faire et Ranger les courses
        cy.contains("Ranger les courses");
    });

    it("Count todos", () => {                       // étpae compter les todos
        cy.contains("Click here to login").click(); // On click sur l'élément HTML qui contient le texte 'Click here to login'
                                                    // !! : il s'agit d'un élément qui ne sert pas à se logger, le texte ne correspond
                                                    // pas à l'action du click sur cet élément
        cy.get("#title").type("RDV dentiste").type("{enter}");      // on simule un press clavier ENTER après avoir écrit RDV dentiste
        cy.get("#title").type("Sortir le chien").type("{enter}");   // on simule un press clavier ENTER après avoir écrit Sortir le chien
        cy.contains("Total Todos: 2");                              // on vérifie que la page HTML contient le texte Total Todos: 2
    });

    it("Check todo", () => {                                                // étape Check todo
        cy.contains("Click here to login").click();                         // click sur l'élément HTML qui contient Click here to login
        cy.get("#title").type("Etre le meilleur dresseur").type("{enter}"); // on simule un press sur ENTER après avoir écrit Etre le meilleur dresseur
        cy.get('[type="checkbox"]').check();                                // on check la check box HTML dont le selecteur CSS est de type checkbox
        cy.contains("Selected Todos: 1");                                   // on vérifie que la page HTML contient le texte Selected Todos: 1
    });
});
```


