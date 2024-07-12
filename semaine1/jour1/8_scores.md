**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

**Semaine 1 - Terminal, Pyhton, Backend**

**Jour 1 : Terminal Commands**

---
# 8 - Scores

## <ins> Traitement des données </ins>

👉 Récupérez la ressource "scores.zip" ci-jointe et unzip-ez la.

👉 Trouvez un moyen d’afficher les colonnes 2 et 4 du fichier scores.txt et stockez-les dans un fichier results.txt.

```
awk '{print $2, $4}' scores.txt > result.txt
```

👉 Trouvez un moyen de calculer la moyenne de toutes les notes présentes dans le fichier results.txt et stockez-la dans un fichier average.txt.

```
awk '{sum += $2; count += 1} END {if (count > 0) print "Average =", sum / count}' results.txt > average.txt
```

> [!TIP]
> sum += $2 : Ajoute la valeur de la deuxième colonne (la note) à la variable sum.  
> count += 1 : Incrémente la variable count pour chaque ligne lue.  
> END {if (count > 0) print "Average =", sum / count} : À la fin de la lecture du fichier, calcule la moyenne en divisant sum par count et affiche le résultat. 
