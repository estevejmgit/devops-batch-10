**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

**Semaine 1 - Terminal, Pyhton, Backend**

**Jour 1 : Terminal Commands**

---
# 6 - Data processing

## <ins> Compter avec le terminal </ins>


👉 Récupérez la ressource "dataprocessing.zip" ci-jointe et unzip-ez la.

👉 Trouvez un moyen de trier les données du fichier testLogs.txt par date et stockez le résultat dans un fichier sortedLogs.txt.

_il faut utiliser l'option -k de sort pour trier par colonne_

```
sort -k2M -k3n -k4 testLogs.txt > sortedLogs.txt
```

👉Trouvez un moyen d’afficher les colonnes 1 et 6 du fichier sortedLogs.txt et stockez-les dans un fichier data.txt.

_avec awk on lui demande de print-er la 1ere et 6e colonne dans le fichier data.txt_

```
awk '{print $1, $6}' sortedLogs.txt > data.txt
```
