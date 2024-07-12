**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

**Semaine 1 - Terminal, Pyhton, Backend**

**Jour 1 : Terminal Commands**

---
# 3 - FILES AND FOLDERS

## <ins> Créer et supprimer dossier </ins>

👉 Récupérez la ressource "filesandfolders.zip" depuis l’onglet dédié sur Ariane.

_Le dossier récupéré contient différents fichiers est assez mal rangé, vous allez mieux l’organiser en vous servant uniquement du terminal_

```
unzip filesandfolders.zip
```

👉 Créez un nouveau dossier appelé "txt" dans le dossier "filesandfolders" via la commande mkdir.


```
cd filesandfolders
mkdir txt
```

Tout compte fait, ranger ensemble les fichiers de logs dans un dossier "txt" ne semble pas très pertinent…

👉 Supprimez le dossier "txt" via la commande rm et créez un répertoire "logs" à la place.


```
rm -r txt/
mkdir logs
```


## <ins> Déplacer un fichiers </ins>

👉 Déplacez le fichier "log1.txt" dans le dossier "logs" via la commande mv.

```
mv log1.txt logs/
```
