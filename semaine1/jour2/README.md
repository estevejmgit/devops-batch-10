   # Formation devOps
_La capsule_

:fire: Exercices et corrections formation devOps :fire:

---
## Semaine 1 :computer: 

Bases du fonctionnement des outils informatiques - Terminal, scripts, notion de serveur backend 

### Jour 2 : Scripting & Droits Linux

---

#### :bike: 1_Execute my script

##### <ins> Création d’un premier script </ins>

Vous utiliserez l’utilitaire nano pour créer vos scripts afin de bénéficier d’un éditeur de texte intégré au terminal.
Pour créer et éditer un nouveau fichier, il suffit d’utiliser la commande suivante : nano nomDuFichier.extension.

:point_right:  Exécutez la commande `nano myscript.sh` et copiez le code suivant dans la fenêtre de l’éditeur de texte :

```bash
#!/usr/bin/env bash
echo "Hello world!"
```

:keyboard: Sauvegardez le fichier en appuyant sur les touches `CTRL + X`, puis en appuyant sur `y` (yes) et enfin sur `Enter`.

##### <ins> Exécution d’un script </ins>

Votre script a bien été créé et vous allez maintenant l’exécuter à l’aide de votre terminal.

Pour cela, la première chose à faire est de donner les droits d’exécution au script.

:point_right: Exécutez la commande suivante.

```bash
chmod +x myscript.sh
```

:keyboard: Sauvegardez le fichier en appuyant sur les touches `CTRL + X`, puis en appuyant sur `y` (yes) et enfin sur `Enter`.

Pour rappel, la commande chmod (abréviation de "change mode") permet de changer les permissions d’un fichier donné. La mention +x indique que nous souhaitons rendre ce fichier exécutable.

:point_right: Exécutez le script contenu dans le fichier myscript.sh avec la commande suivante.

```bash
./myscript.sh
```
