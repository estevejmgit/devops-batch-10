**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

**Semaine 3 - GIT JIRA et CI**

**Jour 3 : CI**

---

# 5 - Friday Alarm

## Pipeline de vérification 

👉 En repartant du répertoire créé dans le challenge précédent créez un nouveau job qui sera en erreur si le commit a lieu un vendredi.

La demande de merge request est donc censée se bloquer automatiquement si elle est faite un vendredi, 
car vous découvrez (ou connaissez) l’adage : on ne met pas un production un vendredi !

👉 Testez le job en modifiant le jour où il est censé être en erreur pour correspondre à aujourd’hui. Vérifiez que la 
demande de merge request échoue également.

```
stages:
  - test

variables:
  API_URL: "https://jsonplaceholder.typicode.com/users"

check_api:
  stage: test
  script:
    - echo "$(date +%u)"
    - echo "Checking if API is reachable"
    - curl $API_URL
    - >
      if [ "$(date +%u)" -eq 5 ]; then 
        echo "Today is Friday. Failing the job."; 
        exit 1; 
      fi
```
