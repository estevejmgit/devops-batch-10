**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

**Semaine 6**

**Jour 3 : Cloud Hosting**

---

# 1 - CDN with cloudfront

## SERVICE DE CDN

Le service CloudFront d’AWS est un CDN (Content Delivery Network) : il fonctionne avec S3 en copiant les fichiers stockés vers 
la périphérie des serveurs d’Amazon pour une récupération rapide grâce à leurs nombreux data centers.

Ce challenge a pour objectif de déployer un site statique où les fichiers et assets seront stockés par S3 tandis que CloudFront 
s’occupera d’attribuer une URL unique (en HTTPS), le tout optimisé grâce au réseau de distribution d’AWS.

👉 Récupérez la ressource "cdnwithcloudfront.zip" ci-jointe.

 👉 Créez un nouveau bucket S3 en le paramétrant de la même façon que le challenge précédent et uploadez le contenu du dossier "ecw-website" via la CLI d’AWS.
