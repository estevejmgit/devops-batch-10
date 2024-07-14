**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

**Semaine 3 - GIT JIRA et CI**

**Jour 3 : CI**

---

# 3 - Flake8

## <ins> Test d'intégration continue </ins>

Les exemples des challenges précédents vous ont permis de découvrir quelques fonctionnalités de GitLab CI/CD. 
Vous allez maintenant appliquer le concept de continuous intégration (CI) en exécutant 
un [linter](https://mindsers.blog/fr/post/linting-good-practices/) de code.

👉 Récupérez la ressource "flake8.zip" ci-joint.

👉 Récupérez le projet Python dans les ressources et hébergez-le sur un nouveau repo GitLab nommé "ultimate-length-app".

_Vous devriez avoir un fichier python qui va afficher la longueur d'une string, à la racine de ultimate-length-app/_

👉 Faites en sorte d’exécuter le linter [Flake8](https://flake8.pycqa.org/) lors d’un push sur n’importe quelle branche.

Pour ce faire, vous aurez sans doute besoin d’utiliser la notion [d’image](https://docs.gitlab.com/ee/ci/docker/using_docker_images.html) 
afin de lancer un job dans un environnement spécifique (avec Python pré-installé, par exemple 😉)

