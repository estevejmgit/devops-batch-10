**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

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
