# Formation devOps

:pill: La capsule

:fire:  Documentation d'accompagnement au cycle devOps :fire:

---


**Semaine 6**

**Jour 3 : Cloud Hosting**

---

# 2 - CDN with cloudfront

## SERVICE DE CDN

Le service CloudFront d’AWS est un CDN (Content Delivery Network) : il fonctionne avec S3 en copiant les fichiers stockés vers 
la périphérie des serveurs d’Amazon pour une récupération rapide grâce à leurs nombreux data centers.

Ce challenge a pour objectif de déployer un site statique où les fichiers et assets seront stockés par S3 tandis que CloudFront 
s’occupera d’attribuer une URL unique (en HTTPS), le tout optimisé grâce au réseau de distribution d’AWS.

👉 Récupérez la ressource "cdnwithcloudfront.zip" ci-jointe.

 👉 Créez un nouveau bucket S3 en le paramétrant de la même façon que le challenge précédent et uploadez le contenu du dossier "ecw-website" via la CLI d’AWS.

```
 aws s3 cp ./ s3://jmeawsbucket/ --recursive
```

 👉 Sur votre bucket S3, trouvez l’option permettant d’activer l’hébergement de site Web statique en précisant le document d’index "index.html".

 

Dans la liste Buckets (Compartiments), choisissez le nom du compartiment pour lequel vous souhaitez activer l'hébergement de sites web statiques.

> Choisissez Propriétés.
> Sous Static website hosting (Hébergement de site Web statique), choisissez Edit (Modifier).
> Choisissez Utiliser ce compartiment pour héberger un site Web.
> Sous Static website hosting (Hébergement de site web statique), choisissez Enable (Activer).
> Dans Index document (Document d'index), entrez le nom du document d'index, généralement index.html. 

 👉 Assurez-vous que chaque objet contenu dans le bucket soit publique en lecture en modifiant la stratégie de compartiment (bucket policy) suivante dans l’onglet "Autorisations".

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::jmeawsbucket/*"
        }
    ]
}
```

 👉 Visitez l’URL statique donnée par S3 en prenant soin d’ajouter "/index.html" à la fin.

> URL dans l'onglet propriété du bucket


 👉 Sur la console du service CloudFront, créez une nouvelle distribution basée le domaine créé par le service S3. Vous pouvez laisser les paramètres par défaut à l’exception de la redirection forcée de HTTP vers HTTPS. N’activez pas le Web Application Firewall (WAF).

> taper cloudfront dans la barre de recherche et suivre les onglets avec les instructons

!! à prendre l'url de la distribution et pas du bucket


