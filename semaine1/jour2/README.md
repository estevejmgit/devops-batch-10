   # Formation devOps
_La capsule_

:fire: Exercices et corrections formation devOps :fire:

---
## Semaine 1 :computer: 

Bases du fonctionnement des outils informatiques - Terminal, scripts, notion de serveur backend 

### Jour 2 : Scripting & Droits Linux

---

#### :bike: 1_my_alias 

##### <ins> Execute my script </ins>

Vous utiliserez l’utilitaire nano pour créer vos scripts afin de bénéficier d’un éditeur de texte intégré au terminal.
Pour créer et éditer un nouveau fichier, il suffit d’utiliser la commande suivante : nano nomDuFichier.extension.

:point_right:  Exécutez la commande `nano myscript.sh`

```bash
cat ls.txt| tr -s [:space:]
```

##### <ins> Créer un Alias </ins>

:point_right:  A partir de la commande alias, créez une nouvelle commande delspace dans votre terminal prenant comme paramètre le nom d’un fichier 
et permettant de supprimer les espaces répétés dans celui-ci.
_Vous pouvez aller jusqu’à insérer cette instruction dans le fichier ".bashrc" à la racine de votre dossier utilisateur afin de
l’utiliser tout le temps, même après avoir relancé le terminal._

- dans le terminal et/ou dans le fichier ~/.bashrc

```bash
alias rm_dbl_space = "cat $1| tr -s [:space:]"  
```

