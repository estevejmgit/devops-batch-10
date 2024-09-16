# Formation devOps

:pill: La capsule

:fire: Documentation d'accompagnement au cycle devOps :fire:

---

## Semaine 2 - BDD, Réseaux, SSH, GIT

### Jour 5 : Démarrer avec Git

- inclure la connection SSH à gitlab dès le début dans le cours serait une bonne idée
- Parler des branches dès le début permettrait de mieux appréhender les concepts nottement cherry-picking
- Faire le point sur les concept de revert, reset, rebase

---

#### :bike: Cherry picking

 Le git cherry-pick est une commande très utile qui permet de sélectionner un ou plusieurs commits spécifiques à partir d'une branche et de les appliquer à une autre branche. Contrairement à une fusion complète (merge), on choisi précisément quel commit on veut transférer, sans apporter tout l'historique d'une branche.

 :world_map: Imaginons que nous travaillons sur deux branches :

- main (la branche principale)
- feature-branch (une branche sur laquelle on développe une nouvelle fonctionnalité)

On réalise qu'un commit  fait dans `feature-branch` serait aussi utile dans `main`. Plutôt que de faire un merge de toute la branche `feature-branch`, on utilise git cherry-pick pour ne récupérer que le commit dont on a besoin.

##### Step by Step

:point_right: Verifier historique des commit dans `feature-branch`

```bash
git log --oneline
```

Sortie :

```bash
z3d5v6z Autre new fonctionnalité
a1b2c3d Nouvelle fonctionnalité terminée
e4f5g6 Bug corrigé dans la fonctionnalité
```

:point_right: on va sur la branche `main` sur laquelle on veut récupérer la fonctionnalité _Nouvelle fonctionnalité terminée_ dont le hash est `a1b2c3d`

```bash
git checkout main
```

:point_right: on applique le cherry-pick avec le hash de la fonctionnalité

```bash
git cherry-pick a1b2c3d
```

:point_right: on va résoudre les conflits si des changements ont été fait par rapport au commit originel commun des deux branches

- On ouvre  les fichiers marqués comme en conflit (Git indique les conflits avec des annotations comme `<<<<<<<branch_current`, `>>>>>>>branch_target`).

- On Résout les conflits en modifiant le code selon ce qui est nécessaire.

- Une fois les conflits résolus, on ajoute les fichiers modifiés :

```bash
git add <fichier_conflit>
```

- On finalise le **cherry-picking**

```bash
git cherry-pick --continue
```

- on vérifie que le commit a bien été pris en compte

```bash
git log --oneline
```
