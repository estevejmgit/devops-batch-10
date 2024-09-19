# Formation devOps

:pill: La capsule

:fire:  Documentation d'accompagnement au cycle devOps :fire:

---

## Semaine 3 :zap:

Versionning avancé avec Git, Jira et intégration continue et tests d'intégration

### Jour 4 : Framework de Test (Cypress)

#### :bike: Cypress begin

##### Installation de Cypress

:point_right: cf Cours

##### Visiter une page

:point_right: cf cours

:point_right: Créez un fichier "wikipedia.cy.js" dans le dossier "e2e" (depuis VS Code) et explorez la
[documentation de Cypress](https://docs.cypress.io/guides/end-to-end-testing/writing-your-first-end-to-end-test) pour construire un scénario qui simulera simplement la navigation vers la page d'accueil de Wikipédia.

```javascript
describe("Testing Wikipedia", () => {          // nom du job courant
    it("Search for content", () => {           // nom de l'étape du job
        cy.visit("https://fr.wikipedia.org/"); // action : visiter le site wikipedia
    });
});
```

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

