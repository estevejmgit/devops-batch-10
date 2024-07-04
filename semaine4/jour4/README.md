# Formation devOps
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

## Semaine 4

### Jour 4 : Azure devOps ###

---

**1 - Azure devOps**



[ ] <ins>### Initialisation ###</ins>

👉 Connectez-vous à Azure DevOps, créez un compte puis une organisation 

> https://aex.dev.azure.com/me

👉 Créez un nouveau projet nommé : “My Flask App”.

> Azure interface

👉 Accédez à l'onglet "Repos" et créez un nouveau repository Git vide.

> Azure interface

👉 Clonez ce [repository](https://github.com/Microsoft/python-sample-vscode-flask-tutorial) sur votre ordinateur.

```
git clone https://github.com/Microsoft/python-sample-vscode-flask-tutorial
cd python-sample-vscode-flask-tutorial
```

> Changez origin pour l'url du repo fournie par azure

```
git remote rm origin
git remote add origin <url_repo_azure>
```

