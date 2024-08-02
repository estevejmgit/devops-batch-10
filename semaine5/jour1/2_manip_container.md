**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

**Semaine 5**

**Jour 1 : Conteneurisation**

---

# 2 - MANIP CONTAINER

Un conteneur Docker est une machine virtualisée légère et autonome, qui comprend tous les éléments nécessaires pour exécuter une application.

👉 Lancez un premier conteneur à partir d’une simple image nommé "hello-word" et créée par l’équipe de Docker. on donne un nom "helloworld" au container

docker run hello-world --name helloworld

👉 Prenez le temps de regarder le retour de la commande précédente. Celle-ci décrit les étapes menées par Docker pour lever le conteneur.

👉 Listez les conteneurs de la machine hôte.

```
docker ps -a
```

👉 Une nouvelle fois, prenez le temps de regarder le retour de la commande précédente.
Celle ci sera très utile afin de voir l’état des conteneurs Docker à tout moment :

   - CONTAINER ID : Identifiant unique du conteneur
   - IMAGE : Image utilisée pour lever le conteneur (ici "hello-world" où son seul rôle sera d’afficher un message sur le terminal)
   - COMMAND : Commande exécutée dans le conteneur ("/hello" qui correspond à un script créé par l’équipe de Docker pour afficher le message que vous avez pu voir tout à l’heure)
   - CREATED : Sans grande surprise, le délai écoulé depuis la création du container
   - STATUS : Information très importante, l’état du container ("exited" car il a été levé, la commande a été exécutée, puis le conteneur a été quitté)
   - PORTS : La liste des ports exposés entre le conteneur et la machine hôte (aucun pour le moment, car ce n’est pas utile)
   - NAMES : Le nom unique de chaque container pour les manipuler plus facilement (il est auto généré par Docker ou spécifié lors de la commande docker run avec l’option --name)

👉 Enfin, supprimez le conteneur via son ID ou directement son nom.

```
docker rm {CONTAINER ID or NAME}
```
