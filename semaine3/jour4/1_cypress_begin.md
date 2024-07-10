**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

**Semaine 3 - GIT JIRA et CI**

**Jour 4 : Cypress**

---

# 1 - CYPRESS BEGIN

## <ins> Install </ins>

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
