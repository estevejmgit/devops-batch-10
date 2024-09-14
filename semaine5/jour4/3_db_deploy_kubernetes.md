# Formation devOps

:pill: La capsule

:fire:  Documentation d'accompagnement au cycle devOps :fire:

---

**Semaine 5**

**Jour 4 : Kubernetes Avancé**

---

# 3 - DB DEPLOYEMENT

## Setup

👉 Créez un manifeste ConfigMap dédié au déploiement d’une base de données PostgreSQL en vous assurant que les contraintes suivantes soient respectées :

- Le ConfigMap sera nommé "mydatabase-config" et dédié à une application nommée "mydatabase"
- Le nom de la base de données par défaut sera "myawesomeapp"
- Le nom d’utilisateur par défaut sera "themiz" avec "IAWAWESOME" comme mot de passe
- Le nom des trois variables d’environnement précédentes devront être conformes à celles utilisées par l’image postgres


👉 Appliquez le manifeste et vérifiez sa création grâce aux commandes habituelles kubectl get et kubectl describe.
