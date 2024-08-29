**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

**Semaine 1 - Terminal, Pyhton, Backend**

**Jour 1 : Terminal Commands**

---
# 1 - MY ALIAS

## <ins> Supprimer Blank Space </ins>

👉 Récupérez la ressource "myalias.zip" ci-jointe.

👉 Trouvez une solution afin de supprimer la répétition d’espaces vides dans le fichier "ls.txt" via la commande tr.

_Utiliser l'option -s_

```
cat ls.txt| tr -s [:space:]
```

## <ins> Créer un Alias </ins>

👉 A partir de la commande alias, créez une nouvelle commande delspace dans votre terminal prenant comme paramètre le nom d’un fichier 
et permettant de supprimer les espaces répétés dans celui-ci.
_Vous pouvez aller jusqu’à insérer cette instruction dans le fichier ".bashrc" à la racine de votre dossier utilisateur afin de
l’utiliser tout le temps, même après avoir relancé le terminal._

- dans le terminal et/ou dans ~/.bashrc

```
alias rm_dbl_space = "cat $1| tr -s [:space:] "  
```
