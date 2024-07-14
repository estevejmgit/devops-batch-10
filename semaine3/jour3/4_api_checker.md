**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

**Semaine 3 - GIT JIRA et CI**

**Jour 3 : CI**

---

# 4 - API Checker

## <ins> Merge requests & pipelines </ins>

L’objectif de ce challenge est de créer un pipeline sur une branche différente (autre que main) afin de vérifier qu’une API 
externe répond et ainsi bloquer une merge request si ce n’est pas le cas.

👉 Créez un nouveau répertoire GitLab nommé "awesome-app", versionnez quelques fichiers (leur contenu n’est pas important pour le 
déroulé du challenge) et faîtes un push sur la branche principale.

👉 Côté GitLab, configurez le répertoire pour que les merge requests soient appliquées (et validables) uniquement lorsque
toutes les pipelines de CI/CD ont réussies.

👉 Sur la branche principale, créez un fichier ".gitlab-ci.yml" qui devra exécuter un job chargé de vérifier qu’une API
(potentiellement utilisée dans le projet) est bien joignable afin de valider l’exécution de la pipeline.

Vous pouvez choisir la "fausse" API JSONPlaceholder et l’endpoint "GET /users".

```
stages:
  - test

variables:
  API_URL: "https://jsonplaceholder.typicode.com/users"

check_api:
  stage: test
  script:
    - echo "Checking if API is reachable..."
    - curl $API_URL
```

