**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

**Semaine 6**

**Jour 3 : Cloud Hosting**

---

# 1 - Storage with S3

## SERVICE DE STOCKAGE

Le service S3 d’AWS est un service de stockage de données en ligne où on peut uploader (télécharger) des fichiers afin de récupérer une URL unique pour chaque fichier.

C’est un des services les plus populaires de la plateforme, car très utilisé par les développeurs pour stocker facilement les assets d’une application.

👉 À partir du service S3, créez un compartiment de stockage (bucket) en lui donnant le nom de votre choix.
Attention, ce nom doit être unique et ne pas être utilisé par un autre compte AWS.

> jmeawsbucket

👉 Lors de la création de votre bucket, laissez les options par défaut à l’exception de l’option "Bloquer tous les accès publics" 
qui doit être décochée : cela permettra de pouvoir stocker vos fichiers et les rendre accessibles depuis internet. 
(cochez checkbox de validation des conditions d'usage)


👉 Récupérez la ressource "storagewiths3.zip" ci-joint.

*👉 Parmi toutes les images présentes dans le dossier "wwe", 
choisissez-en une seule afin de l’uploader vers S3 en laissant les options par défaut afin que le fichier soit public.

 👉 Assurez-vous que chaque objet contenu dans le bucket soit publique en lecture en modifiant la stratégie de compartiment (bucket policy) suivante dans l’onglet "Autorisations" du Bucket

```
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "PublicReadgetObject",
			"Principal": "*",
			"Effect": "Allow",
			"Action": "s3:GETObject",
			"Resource": "arn:aws:s3:::jmeawsbucket/*"
		}
	]
}
```

👉 Trouvez un moyen de récupérer l’URL publique du fichier précédemment uploadé et vérifiez que vous pouvez visionner l’image en ouvrant une nouvelle fenêtre en navigation privée.

👉 Via la CLI d’AWS, trouvez un moyen d’uploader tout le contenu du dossier "wwe" vers votre bucket.

> AWS CLI put-object reference

```
aws s3 cp ./ s3://jmeawsbucket/ --recursive
```

👉 Vérifiez que l’upload a bien réussi en listant les objets présents, toujours via la CLI d’AWS.

```
aws s3 ls s3://jmeawsbucket/ --recursive
```

👉 delete all content from bucket for specific version :

```
aws s3api delete-objects --bucket jmeawsbucket \ 
  --delete "$(aws s3api list-object-versions \
  --bucket "jmeawsbucket" \
  --output=json \
  --query='{Objects: Versions[].{Key:Key,VersionId:VersionId}}')"
```

for  all versions :

```
aws s3 rm s3://jmeawsbucket --recursive
```
