# Formation devOps
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

## Semaine 4

:tanabata_tree: Déploiement continu, tests de déploiement, Provider Cloud Azure DevOps 

### Jour 2 : Test de montée en charge ###

---

#### :bike: 1_Test de montée en charge

##### <ins> Install </ins>

👉 [Installer Django](https://ariane.lacapsule.academy/batch/slide/65f2c8bfd81f64001d211e68) et démarrer le serveur

👉 [Installer Locust](https://docs.locust.io/en/stable/installation.html)

##### <ins> 1er test Locust </ins>

👉 À la racine de votre dossier projet, créez un nouveau fichier appelé "locustfile.py" contenant le code suivant.

```python
from locust import HttpUser, task

class First_Load_Test(HttpUser):
    @task
    def first_test(self):
        self.client.get("/")
```

👉 Dans le même dossier, exécutez la commande suivante qui ouvrira par défaut le test contenu dans "locustfile.py".  

```bash
locust
```

👉 Découvrez l’interface web de Locust en visitant l’URL suivante : http://localhost:8089
( ~~https~~ ) 

**Locust config :**

- Nb peak user
- Nb new user / s
- Execution time

##### <ins> Locust en ligne de commande </ins>

👉 Lancez un nouveau directement depuis le terminal en précisant les mêmes informations en ligne de commande.

```bash
locust --headless --users 10 --spawn-rate 1 -H http://IP:PORT -t 15s
```

Vous l’avez sans doute remarqué, le résultat affiché sur le terminal est assez peu lisible…

👉 Trouvez une option à la CLI de Locust afin de n’afficher que le résumé à la fin du test de montée en charge.

```bash
--only-summary
```

---

#### :bike: 2_Stand The Line

_Dans ce challenge, vous allez jouer ce scénario dans vos tests avec Locust [??? et Cypress ???] afin de vous assurer que le système de queue mis en place est fonctionnel._

##### <ins> Setup de l'app </ins>

👉 Récupérez le code source du serveur de l’application e-commerce sur GitLab 

1 Créer un dossier bikeshop
2 Cloner le repo git dans le bikeshop \

```bash
git clone https://gitlab.com/la-capsule-bootcamp/bikeshop
```

👉 Positionnez-vous dans le dossier et installez les dépendances (vous pouvez utiliser yarn ou npm avec Node.js).

```bash
npm install
```

👉 Lancez le serveur et vérifiez qu’il fonctionne en visitant la page http://localhost:3000 dans votre navigateur.

```bash
npm start
```

##### <ins> Load testing de l'app </ins>

👉 Lancez un test de montée en charge sur la page "/" du serveur avec 1000 utilisateurs qui visitent le site en simultané pendant 20s (à raison de 20 utilisateurs toutes les secondes).

```bash
locust --headless --only-summary --users 1000 --spawn-rate 20 -H http://IP:PORT -t 20s
```

👉 Une fois le test de montée en charge lancé avec Locust, visitez la page d'accueil de l’application depuis votre navigateur afin de vérifier si vous êtes bien redirigé vers la file d’attente.

👉 Vous pouvez éteindre le serveur Node.js (via Ctrl + C) et le relancer pour réinitialiser le décompte des requêtes. Revisitez alors le site via votre navigateur.

---

#### :bike: 3_Locust In My Pipeline

##### <ins> Création d'une pipeline </ins>

👉 Reprenez le dépôt local du challenge précédent.

👉 Retirez le lien avec le dépôt distant.

👉 Créez un nouveau repository GitLab nommé "bikeshop" et liez-le à votre dépôt local.

👉 Poussez la branche master sur le dépôt distant.

```bash
git remote set-url origin <git url>
git push origin master
```

👉 À partir de GitLab CI/CD, créez une pipeline capable de lancer Locust pour un test de montée en charge avec 100 utilisateurs qui visitent le site en simultané pendant 5s (à raison de 20 utilisateurs toutes les secondes).

Vous devrez préciser l’image Docker suivante (à la première ligne) afin de partir sur un worker Linux avec Node.js et Python préinstallés : **image: nikolaik/python-nodejs:latest**

> [!NOTE]
> Assurez-vous que la CLI de Locust et les dépendances du serveur Node.js soient installés, mais aussi que ce dernier soit démarré en tâche de fond (avec le & en fin de commande)

```yaml
image: nikolaik/python-nodejs:latest

stages:
  - test

jobs:
  stage: test
  script:
  - pip3 install locust
  - npm install
  - npm start &
  - locust --headless --only-summary --users 100 --spawn-rate 20 -H http://localhost:3000 -t 5s
```

> [!WARNING]  
> Ne pas oublier d'ajouter un fichier locustfile.py _(voir 1 - LOADING TEST)_ à la racine du projet

---

#### :bike: 4_DDOS Attack

##### <ins> Attaque par dénis de service </ins>

_Afin de vous rendre compte des possibilités et de la puissance de Locust, vous allez vous mettre pendant quelques instants dans la peau d’un véritable hacker en menant une attaque DDoS sur votre propre serveur !_

👉 Installez le package Linux htop afin de superviser les ressources de la machine.

👉 Créez un nouveau dossier nommé "ddosattack" qui pourra contenir le(s) fichier(s) de ce challenge.

👉 Trouvez un moyen de démarrer un simple serveur web local sur le port 8585 via le module http-server de Python (à l’aide d’une seule commande sur le terminal).

```bash
python3 -m http.server 8585
```

👉 Une fois le serveur web démarré, créez un test de montée en charge assez conséquent et analysez les courbes sur l’onglet "Charts", notamment le temps de réponse.

```bash
locust --headless --only-summary --users 1000 --spawn-rate 20 -H http://IP:PORT -t 20s
```

> [!WARNING]  
> Ne pas oublier d'ajouter un fichier locustfile.py _(voir 1 - LOAD TEST)_ à la racine du projet

👉 Arrêtez le test de montée en charge pour le moment et lancez le programme htop afin de monitorer la charge du système en temps réel.

👉 Gardez un œil sur le monitoring du système et relancez le test de montée en charge afin de constater des ressources utilisées par le serveur web (et non pas par Locust qui est censé être plus gourmand).
