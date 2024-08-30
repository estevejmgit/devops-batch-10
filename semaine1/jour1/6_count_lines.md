**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

**Semaine 1 - Terminal, Pyhton, Backend**

**Jour 1 : Terminal Commands**

---
# 5 - COUNT LINES

## <ins> Compter avec le terminal </ins>


👉 Récupérez la ressource "countlines.zip" ci-jointe et unzip-ez la.

👉 Affichez le contenu du répertoire via la commande ls.

```
ls countlines/
```

 👉 Stockez le résultat de la commande précédente dans un fichier "numberLines.txt". 

 
```
ls countlines/ > numberLines.txt
```

👉 Comptez le nombre de lignes présentes dans le fichier "numberLines.txt".  
_Utiliser la fonction `wc` (pour word count) avec l'option `-l` (pour line)_

```
wc -l numberLines.txt
```

