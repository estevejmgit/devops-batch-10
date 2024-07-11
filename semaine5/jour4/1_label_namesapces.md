**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

**Semaine 5**

**Jour 4 : Kubernetes Avancé**

---

# 1 - LABEL et NAMESPACES

👉 Les labels sont des données de type clé/valeur qui sont attachés aux objets permettant de les identifier plus facilement.

Si vous regardez d’un peu plus près le contenu d’un des fichiers de déploiement que vous avez créé, vous remarquerez que la partie "metadata" contient un tableau "labels" possédant une étiquette "app".

```
apiVersion: apps/v1

kind: Deployment
metadata:
  name: httpd-server-deployment
  labels:
    app: httpd-server
spec:
  replicas: 4
  selector:
    matchLabels:
      app: httpd-server
  template:
    metadata:
      labels:
        app: httpd-server
    spec:
      containers:
      - name: httpd-server
        image: httpd:latest
        imagePullPolicy: Always
        ports:
        - containerPort: 80
```

👉 Déployez le manifeste ci-dessus et listez tous les pods du cluster avec l’option "--show-labels".
Le label "app=httpd-server" est censé s’afficher à côté de chaque pod lié au manifeste de déploiement.

👉 Trouvez la commande kubectl permettant de lister les pods en appliquant un filtre sur le label "app" afin de ne voir que les pods liés à notre application "httpd-server".
