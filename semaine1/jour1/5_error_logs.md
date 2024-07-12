**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

**Semaine 1 - Terminal, Pyhton, Backend**

**Jour 1 : Terminal Commands**

---
# 5 - FILTER LOGS

## <ins> Filtrer les logs </ins>


👉 Récupérez la ressource "errorlogs.zip" ci-jointe et unzip-ez la.

👉 Stockez contenu de l’ensemble des fichiers log.txt présents dans le répertoire "errorlogs" dans le fichier globalLogs.txt.

```
cat log*.txt > globalLogs.txt
```

👉 Filtrez le contenu du fichier globalLogs.txt pour n’afficher que les lignes contenant la mention WARNING.

```
grep WARNING globalLogs.txt 
```

👉 Stockez le résultat de la commande précédente dans un fichier warningLogs.txt.


```
grep WARNING globalLogs.txt > warnings.txt
```

👉 Supprimez le fichier globalLogs.txt.


```
rm -f globalLogs.txt
```
