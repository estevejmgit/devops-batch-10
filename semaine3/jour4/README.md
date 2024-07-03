# Formation devOps
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

## Semaine 3 - GIT JIRA et CI

### Jour 4 : Cypress ###

---

**1 - CYPRESS BEGIN**

[ ] <ins>### Install ###</ins>

Un test end-to-end (e2e) est un test logiciel qui a pour but de valider que le système testé répond 
correctement à un cas d’utilisation, mais également de vérifier l’intégration de ce cas dans l’interface.
L’intérêt de ces tests est de s’assurer qu’une fonctionnalité développée répond à la demande du point de 
vue de l’utilisateur.

Ce challenge constitue l’occasion de prendre en main le fonctionnement global de [Cypress](https://docs.cypress.io/guides/overview/why-cypress).*

👉 Installez et configurez l’environnement d’exécution JavaScript Node.js en exécutant les 7 commandes suivantes.

```
sudo apt remove nodejs npm -y

curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.2/install.sh | bash
echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p

source ~/.bashrc
nvm install stable

nvm use stable
npm install -g yarn
```

👉 Créez un nouveau dossier "cypressbegin" dans lequel vous initialisez un nouveau projet Node.js.

```
npm init -y
```

👉 Ajoutez les lignes suivantes dans le fichier "package.json" (à la place de l’objet "scripts" déjà présent).

```
"scripts": {

  "test": "npx cypress run --config video=false",

  "cypress:open": "npx cypress open"

},
```

👉 Lancez Cypress avec la commande suivante.

```
yarn run cypress:open
```

👉 Sélectionnez le testing end-to-end (e2e) puis le navigateur "Electron".

👉 Cypress est désormais installé. Sélectionnez l’option **"Scaffold example specs"** afin de générer des tests d’exemple. 

👉 Avant de construire vos propres tests, ces specs d’exemple vous donneront un bon aperçu du 
fonctionnement de Cypress et de sa syntaxe. Vous retrouvez les tests dans le dossier "cypress/e2e".

👉 Sur l’onglet "Specs", sélectionnez une suite de tests (finissant par .cy.js) et cliquez
pour ouvrir le test runner qui exécutera le test. Sachez qu’il est également possible de lancer 
un test sans passer par l’interface graphique, directement depuis le terminal.

👉 Avant de passer à l’étape suivante, **supprimez tout le contenu du dossier "e2e"**.


[ ] <ins>### Visiter une page ###</ins>

Comme nous l’avons vu durant la journée consacrée à la gestion de projet, les user stories, au cœur du 
framework Agile, reposent sur un format qui ressemble à : "En tant qu’utilisateur, j’effectue cette 
action pour obtenir ce résultat".

Pour effectuer un test sur cette user story, vous allez simuler l'action de l’utilisateur à travers le test, 
puis vous assurer que l'état de l'application qui en découle correspond à vos attentes.

```
Les tests prennent la structure suivante :
describe("Nom de la suite de tests", () => {
  it("Nom du scénario", () => {

        // Code du scénario …

  });
});
```

👉 Créez un fichier "wikipedia.cy.js" dans le dossier "e2e" (depuis VS Code) et explorez la [documentation de Cypress](https://docs.cypress.io/guides/end-to-end-testing/writing-your-first-end-to-end-test)
pour construire un scénario qui simulera simplement la navigation vers la page d'accueil de Wikipédia.

```
describe("Mes 1er CY tests", () => {
    it("test_visit_wiki", () => {
        cy.visit("https://wikipedia.fr")
    })
})
````


👉 Lancez le test depuis le terminal grâce à la commande suivante.

```
yarn test
```

👉 Vous pouvez également lancer le test dans le test runner (via l’interface graphique) pour visualiser l’exécution des instructions dans le navigateur.

```
yarn run cypress:open
```
