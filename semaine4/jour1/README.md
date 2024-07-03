# Formation devOps
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

## Semaine 4

### Jour 1 : Déploiement continu ###

---

**1 - GITLAB PAGES**

[ ] <ins>### Déploiement d’un site statique ###</ins>

Les [GitLab Pages](https://docs.gitlab.com/ee/user/project/pages/) permettent de publier un site 
statique directement à partir d’un repository GitLab. Cette méthode est souvent utilisée pour les 
projets open sources ou les équipes de développement qui souhaitent publier une documentation liée à leur dépôt GitLab.

Dans votre cas, les GitLab Pages seront très utiles pour vous entraîner à déployer un simple site web.

👉 Créer un répertoire GitLab nommé "mystaticpage" et suivez la [documentation](https://docs.gitlab.com/ee/user/project/pages/getting_started/pages_from_scratch.html) 
afin de créer une GitLab Page via le générateur de site statique (SGG) Jekyll.

Résumé : \
1 create empty repo gitlab and clone locally \
2 create index.html with any html \
3 create Gemfile and populate :
```
source "https://rubygems.org"

gem "jekyll"
```
4 create .gitlab-ci.yml and populate :
```
image: ruby:3.2

pages:
  script:
    - gem install bundler
    - bundle install
    - bundle exec jekyll build -d public
  artifacts:
    paths:
      - public
```

👉 Après avoir suivi les étapes de création des fichiers du projet (dont le fichier ".gitlab-ci.yml"), 
poussez vos commits vers la branche main afin de lancer le job chargé de déployer le site en statique.

--> allez vérifier la pipeline sur gitlab

👉 Enfin, vérifiez que le site statique a bien été déployé en visant l’URL donnée sur GitLab dans "Deploy > Pages".

---

**2 - DEPLOY TO VERCEL**

[ ] <ins>### Install ###</ins>

Il existe peu de façons d’héberger son code source en ligne (GitHub, GitLab, Bitbucket…), mais à contrario, 
il existe une multitude de plateformes capables d’héberger une application frontend et/ou backend.

À travers ce challenge, vous allez découvrir [Vercel](https://vercel.com/), une plateforme assez appréciée par les développeurs 
et les DevOps car elle capable de déployer une application frontend très facilement et sans passer par une pipeline complexe de CI/CD.

👉 Créez un projet GitLab nommé "pokedex" et clonez le localement

👉 Créez trois fichiers index.html, script.js et style.css  dans ce dossier et poussez les vers le dépôt distant



<details>
	<summary>index.html</summary>
	
```
<!DOCTYPE html>
<html>

<head>
	<link rel="stylesheet" href="style.css" />
	<title>Hello La Capsule</title>
</head>

<body>
	<h1>Pokedex</h1>

	<div id="pokemonContainer">
		<div class="pokemon electric">
			<div class="imgContainer">
				<img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/25.png" alt="Pikachu" />
			</div>
			<div class="info">
				<h3 class="name">Pikachu</h3>
				<span class="type">Type: <span>electric</span></span>
			</div>
		</div>
	</div>

	<button id="next">Next</button>

	<script src='script.js'></script>
</body>

</html>
```

</details>


<details>
	<summary>script.js</summary>
	
```
let startIndex = 1;
let pokemonsNumber = 15;

function createPokemonCard(pokemon) {
  const type = pokemon.types[0].type.name;
  const name = pokemon.name[0].toUpperCase() + pokemon.name.slice(1);

  document.querySelector('#pokemonContainer').innerHTML += `
    <div class="pokemon ${type}">
      <div class="imgContainer">
        <img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${pokemon.id}.png" alt="${name}" />
      </div>
      <div class="info">
        <h3 class="name">${name}</h3>
        <small class="type">Type: <span>${type}</span></small>
      </div>
    <div>
  `;
}

function fetchPokemons() {
  for (let i = startIndex; i <= pokemonsNumber; i++) {
    fetch(`https://pokeapi.co/api/v2/pokemon/${i}`)
      .then(response => response.json())
      .then(data => {
        createPokemonCard(data);
      });
  }
}

document.querySelector('#next').addEventListener('click', function () {
  startIndex += pokemonsNumber;
  pokemonsNumber += pokemonsNumber;
  fetchPokemons();
});

// Initial fetch
fetchPokemons();
```
</details>


<details>
	<summary>style.css</summary>

```
@import url('https://fonts.googleapis.com/css?family=Lato:300,400&display=swap');

body {
	background: #EFEFBB;
	background: -webkit-linear-gradient(to right, #D4D3DD, #EFEFBB);
	background: linear-gradient(to right, #D4D3DD, #EFEFBB);
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
	font-family: 'Lato';
	margin: 0;
}

h1 {
	letter-spacing: 3px;
}

#pokemonContainer {
	background-color: '#fceaff';
	display: flex;
	flex-wrap: wrap;
	align-items: space-between;
	justify-content: center;
	margin: 0;
	max-width: 1200px;
}

.pokemon {
	background-color: #eee;
	border-radius: 20px;
	box-shadow: 0 3px 15px rgba(100, 100, 100, 0.5);
	margin: 10px;
	padding: 20px;
	text-align: center;
}

.pokemon .imgContainer {
	background-color: rgba(255, 255, 255, 0.6);
	border-radius: 50%;
	width: 120px;
	height: 120px;
	text-align: center;
}

.pokemon .imgContainer img {
	margin-top: 20px;
	max-width: 90%;
}

.pokemon .info {
	margin-top: 20px;
}

.pokemon .name {
	margin: 15px 0 7px;
	letter-spacing: 1px;
}

#next {
	font-weight: bold;
	background-color: rgba(255, 255, 255, 0.6);
	border-radius: 15%;
	width: 80px;
	height: 40px;
	margin: 20px;
}

.normal {
	background-color: #f5f5f5;
}

.fire {
	background-color: #fddfdf;
}

.grass {
	background-color: #defde0;
}

.electric {
	background-color: #fcf7de;
}

.water {
	background-color: #DEF3FD;
}

.ground {
	background-color: #f4e7da;
}

.rock {
	background-color: #d5d5d4;
}

.fairy {
	background-color: #fceaff;
}

.poison {
	background-color: #98d7a5;
}

.bug {
	background-color: #f8d5a3;
}

.dragon {
	background-color: #97b3e6;
}

.psychic {
	background-color: #eaeda1;
}

.flying {
	background-color: #f5f5f5;
}

.fighting {
	background-color: #e6e0d4;
}
```
 
</details>



[ ] <ins>### Déploiement d'une application web ###</ins>

👉 Déployez l’application vers Vercel.

1 Allez sur https://vercel.com/new \
2 Choisissez import git repo > Gitlab \
3 authorisez l'accès \
4 importez le répo **"pokedex"** \
5 spécifiez une URL d'accès

👉 Une fois le site déployé, visitez-le afin de vérifier que tout s’est bien passé.

_Sur l'URL d'accès spécifiée au-dessus en point 5_

👉 Modifiez le nom de domaine attribué par Vercel afin de suivre le format suivant : pokedex-votreprenom-datedujour.vercel.app (par exemple : pokedex-antoine-2512.vercel.app)

_Dans Project > Setting > Domains_

👉 Modifiez le fichier "index.html" et poussez votre commit vers la branche main.

_Vercel est censé trigger le changement et re-déployer l’application ! Magique n’est-ce pas ? 🪄_

👉 Par défaut, Vercel déploie la branche main. Modifiez ce paramètre pour que la branche "prod" soit déployée.

_Dans Project > Setting > Git > Production Branch_

👉 Depuis GitLab, créez la branche "prod" afin de vérifier si l’étape précédente a bien été réalisée.

Pour conclure, il est tout à fait possible de créer plusieurs projets Vercel pour un seul répertoire git afin de multiplier les environnements (test, pré-production, production)

---

**3 - DEPLOYMENT PREVIEW**

[ ] <ins>### Environnement de preview ###</ins>

Vercel est également capable de gérer des environnements de preview (parfois appelés pre-prod) 
qui sont utiles pour essayer une nouvelle fonctionnalité dans en environnement semblable à celui de production.

👉 Reprenez le répertoire GitLab créé dans le challenge précédent.

👉 Créez une nouvelle branche nommée "newfeature" et faîtes une modification dessus. Poussez cette branche vers GitLab.

👉 Faîtes une demande de merge request de la branche "newfeature" vers "prod" et récupérez l’URL de preview donnée par Vercel en commentaire afin de la visiter.

---

**4 - PROTECTED BRANCH**

[ ] <ins>### Protection des branches ###</ins>

👉 Récupérez la ressource "protectedbranches.zip" depuis [l’url](https://static.lacapsule.academy/programs/devops-full-time/J19/protectedbranches.zip) sur Ariane.

👉 Créez un répertoire GitLab nommé "protectedbranches" et poussez le code précédemment récupéré sur "main" ainsi qu'une nouvelle branche "prod".

👉 Déployez l’application vers Vercel, uniquement à partir de la branche "prod".

1 Allez sur https://vercel.com/new \
2 Choisissez import git repo > Gitlab \
3 authorisez l'accès \
4 importez le répo **"protectedbranches"** \

👉 Visitez l’URL "/api" sur le site en production. Une réponse en JSON est censée être affichée.

👉 Mettez-vous dans la peau d’un développeur inexpérimenté (ou maladroit) en supprimant le code de la ligne 4 à 6 dans le fichier "routes/index.js" puis poussez directement sur la branche "prod".

👉 Visitez de nouveau l’URL "/api". Une erreur est censée s’afficher.

Problème : le site en production crash et personne n’a pu vérifier le problème en amont car il est possible de push directement sur la branche "prod", sans passer par une merge request.

👉 À partir de GitLab, protégez la branche "prod" afin de forcer la création d’une merge request lors d’une mise en production.

To protect a branch:

1    On the left sidebar, select Search or go to and find your project. \
2    Select Settings > Repository. \
3    Expand Protected branches. \
4    Select Add protected branch. \
5    From the Branch dropdown list, select the branch you want to protect. \
6    From the Allowed to merge list, select a role that can merge into this branch. \
7    From the Allowed to push and merge list, select a role that can push to this branch.  \
8    Select Protect.  \

---

**5 - PRODUCTION LOGS**

[ ] <ins>### Tests d'intégration continue ###</ins>

Les exemples des challenges précédents vous ont permis de découvrir quelques fonctionnalités de GitLab CI/CD. Vous allez maintenant appliquer le concept de continuous intégration (CI) en exécutant un [linter](https://mindsers.blog/fr/post/linting-good-practices/) de code.

👉 Récupérez la ressource "productionlogs.zip" depuis [l’url](https://static.lacapsule.academy/programs/devops-full-time/J19/productionlogs.zip) sur Ariane.

👉 Créez un répertoire GitLab nommé "productionlogs" et poussez le code précédemment récupéré.

👉 Déployez l’application vers Vercel.

1 Allez sur https://vercel.com/new \
2 Choisissez import git repo > Gitlab \
3 authorisez l'accès \
4 importez le répo **"protectedbranches"** \

👉 Visitez l’URL "/api" et constatez que le navigateur vous renvoie une erreur peu parlante : "Internal Server Error".

👉 Vérifiez si le déploiement s’est bien passé en commençant par regarder côté GitLab, puis côté Vercel dans l’onglet "Deployments".

👉 Le déploiement semble s’être bien passé. Regardez du côté des logs, sur la page du projet bouton "Runtime logs" et relancez une requête afin de déterminer la cause du problème.

```
fichier ./routes/index.js > erreur manque un "m" à la variable "message" ligne 6
```

👉 Une fois l’erreur identifiée et même si celle-ci doit être réglée par l’équipement de développement, corrigez-là.
