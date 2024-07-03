# Formation devOps
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

## Semaine 3 - GIT JIRA et CI

### Jour 5 : Jest ###

---

**1 - JEST BEGIN**

[ ] <ins>### Install ###</ins>

Vous avez eu l’occasion de découvrir la notion de test end-to-end avec Cypress et il est maintenant temps de se focaliser sur un type de test en particulier : les tests unitaires, qui font partie intégrante de la notion de tests e2e.

Les tests unitaires ont pour seul objectif de vérifier le retour d’une fonction créée par les développeurs, sans pour autant vérifier son intégration dans le projet d’un point de vue utilisateur final.

Ce challenge constitue l’occasion de prendre en main le fonctionnement global de Jest, un framework de tests unitaires pour les projets web & mobile en JavaScript.

👉 Récupérez la ressource "jestbegin.zip" ci-jointe, dézipez là dans le répertoire du projet.

Cette archive contient un simple projet JavaScript avec quelques fonctions qui permettent d’effectuer l’addition, la soustraction ou la multiplication de deux nombres.

👉 En vous basant sur la [documentation](https://jestjs.io/docs/getting-started), installez Jest via la commande npm, tout en étant positionné dans le répertoire du projet.

```
npm install --save-dev jest
```

👉 Ajoutez la section suivante dans le fichier "package.json" afin que la commande yarn test puisse exécuter Jest.

```
"scripts": {

  "test": "jest"

},
```


[ ] <ins>### Lancement des tests ###</ins>

👉 Lancez les tests Jest avec la commande suivante.

```
yarn test
```

Vous êtes censés voir que le premier test intitulé "Addition - 5 + 6 = 11" a été validé.

👉 Ouvrez le fichier "calc.test.js" et identifiez la partie responsable de la vérification du bon fonctionnement de la fonction "addition”.

Dans calc.test.js : 

```
const { addition } = require('./calc');

test('Addition : 5 + 6 = 11', () => {
  expect(addition(5, 6).toBe(11));
});
```

Dans calc.js :


```
function addition(a, b) {
  return a + b;
}

module.exports = { addition };
```

---

**2 - JEST MEETS GITLAB**

[ ] <ins>### Install ###</ins>

Vous allez récupérer les tests unitaires du challenge précédent et automatiser l’exécution de ces tests dans une pipeline GitLab.

⚠️ Attention : GitLab limite l’usage de ses outils CI/CD à 400 minutes dans sa version gratuite.
Évitez les pushs inutiles et vérifiez bien que les jobs ne durent pas plus de quelques minutes (dans l’onglet CI/CD > Jobs) et stoppez les jobs qui ne sont pas nécessaires.

👉 Hébergez le projet du challenge précédent sur GitLab.


[ ] <ins>### Création d'une pipeline ###</ins>

👉 Créez un fichier ".gitlab-ci.yml" chargé d’exécuter les tests Jest à chaque commit.

_Vous devrez choisir l’image Docker la plus adaptée par rapport à l’environnement du projet (NodeJS)_

```
image: node:22-alpine3.19

stages:
  - test

jobs:
  stage: test
  script:
  - yarn test
```

👉 Une fois la pipeline créée, effectuez un push vers GitLab et suivez les logs du job en cours afin de vérifier que le runner exécute bien les tests.

👉 Modifiez un des tests afin de vérifier que la pipeline est bien en erreur lorsqu’un test n’est pas validé.
