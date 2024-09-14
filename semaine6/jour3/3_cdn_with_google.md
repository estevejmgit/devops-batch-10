# Formation devOps

:pill: La capsule

:fire:  Documentation d'accompagnement au cycle devOps :fire:

---


**Semaine 6**

**Jour 3 : Cloud Hosting**

---

# 3 - CDN with google

## SERVICE DE CDN


👉 Récupérez la ressource "cdnwithcloudfront.zip" du challenge précédent.

👉 À partir de Google Cloud Console, créez un bucket dans Google Cloud Storage :

- Nommez le bucket de manière unique.

- Laissez les options par défaut, mais assurez-vous que l'option "Uniform bucket-level access" est activée pour faciliter l'accès public.

👉 [installer gcloud CLI sur votre machine](https://cloud.google.com/sdk/docs/install?hl=fr)

- Init connnection :

```
gcloud init (follow instructions)
```

- list buckets :

```
gcloud storage ls
```

👉 Uploadez le contenu du dossier “ecw-website” sur votre bucket en utilisant le CLI de Google Cloud SDK

```
gsutil cp -r <SRC_PATH> gs://<BUCKET_NAME>/
```

👉 Configurez votre bucket afin d’activer l'hébergement de site statique.

> Bucket onglet authorisation


👉 Utilisez Google Cloud Load Balancer pour créer un CDN avec Google Cloud CDN activé. Assurez-vous que le backend service est connecté à votre bucket.

Onglet Backend du load balancer HTTP > créer un line bucket avec le nom du bucket céer ci-dessus

👉 Accédez à l'URL fournie par le Load Balancer pour tester le CDN.

👉 Supprimez toutes les ressources créées après vérification pour éviter les coûts supplémentaires
