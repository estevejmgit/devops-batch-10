# Formation devOps

:pill: La capsule

:fire:  Documentation d'accompagnement au cycle devOps :fire:

---

## Semaine 6 :cloud: 

Cloud Computing AWS, Google GCE, Azure VM, Communication entre les instances


### Jour 1 : Hosting & Cloud

#### :bike: The IT Cloud

##### Création et configuration du compte AWS

👉 Créez un compte sur AWS.com en suivant ces étapes :

Choisissez "Personnel" à la question “Comment prévoyez-vous d'utiliser AWS ?"
Remplissez vos informations personnelles et de paiement, elles ne seront utilisées que pour bloquer 1$ pendant quelques jours afin d’éviter les fraudes et activer l’offre gratuite

À travers sa plateforme, AWS offre plus de 200 services capables de couvrir tous les besoins potentiels d’une application dans l’internet d’aujourd’hui.

Rassurez-vous, même si on peut rapidement se perdre dans AWS, vous aurez toujours une liste des services récents et favoris pour vous y retrouver facilement.

👉 Recherchez "AWS Budgets" dans la barre de recherche des services et rendez-vous sur la partie "Modes de paiement" dans "Préférences" afin de vérifier que les informations de facturation ont bien été validées et que votre identité a bien été vérifiée.

👉 Toujours sur le service AWS Budgets, grâce à l’outil "Budgets" dans la partie "Cost Management", créez un budget qui vous alertera par mail dès que vos dépenses dépassent les limites de l'offre gratuite d'AWS.

##### Création et configuration du compte Google Cloud Platform

👉 Créez un compte sur GCP en suivant ces étapes :

Rendez-vous sur https://cloud.google.com et cliquez sur "Essai gratuit".
Entrez vos informations personnelles et de paiement (elles ne seront utilisées que pour une vérification et ne seront pas facturées tant que vous utilisez les ressources gratuites).

👉 Accédez à la console GCP à https://console.cloud.google.com.

👉 Configurez les alertes de budget :

Dans la console GCP, recherchez et sélectionnez "Facturation".
Allez dans "Budgets & alertes" et créez un nouveau budget.
Configurez les seuils qui déclencheront les alertes pour vous prévenir lorsque vos coûts approchent ou dépassent le montant que vous avez défini (par exemple, le plafond de l'essai gratuit).

##### Création et configuration du compte Microsoft Azure

👉 Créez un compte sur Microsoft Azure en suivant ces étapes :

Visitez https://azure.microsoft.com et cliquez sur "Démarrer gratuitement".
Entrez vos informations personnelles et de paiement pour la vérification ; une petite transaction peut être temporairement retenue pour authentifier le compte.

👉 Configurez les alertes de coût et de budget :

Dans le portail Azure, naviguez vers "Gestion des coûts et facturation".
Sélectionnez "Budgets" dans le menu et cliquez sur "Ajouter".
Définissez les paramètres de votre budget pour recevoir des alertes lorsque vos dépenses atteignent ou dépassent les limites préconfigurées, pour éviter des dépenses inattendues au-delà de l'offre gratuite.

#### :bike: Virtual servers with EC2

##### Création d’une instance EC2

Le service EC2 permet de louer des serveurs virtuels sur lesquels vous pouvez par exemple héberger des applications web en production, on parle alors de serveur de production.

Le fonctionnement de AWS est basé sur un système de régions basé sur les différents centres de données (data center) d’Amazon partout dans le monde.

La plupart du temps, lorsque vous louez ou utilisez un service AWS, il est rattaché à une région.

👉 Même si vous disposez de l’offre gratuite, comparez les tarifs des instances EC2 en Europe afin de choisir la région la moins chère pour une instance de type "t3.micro".

👉 Sur la console AWS, en haut à droite, sélectionnez la région choisie dans l’étape précédente.
Veillez à toujours vérifier quelle région est sélectionnée sur la console, car une instance EC2 créée dans une région ne sera pas visible pour une autre région, tout est compartimenté.

👉 Préparez le lancement d’une instance EC2 en sélectionnant et remplissant les informations suivantes :

- Nom : myfirstvps
- Système d’exploitation : Debian 12, 64 bits (x86)
- Type d’instance : t3.micro
- Paramètres réseau : "Sélectionner un groupe de sécurité existant" > "default"
- Configurer le stockage : 15 Gio
- Nombre d’instances : 1

👉 Pour la partie "Paire de clés (connexion)", créez une nouvelle paire de clés SSH portant le même nom que l’instance que vous vous apprêtez à créer, avec les options par défaut.

Gardez bien de côté le fichier .pem (clé privée) qui se télécharge à la création de la paire de clé, il vous sera utile pour vous connecter au serveur.

👉 Consultez le résumé puis lancez l’instance EC2. Cela ne devrait prendre que quelques secondes grâce à la magie du cloud ☁️

👉 Vérifiez que l’instance a bien été créée et que son état est bien "En cours d’exécution" à partir du menu "Instances".

##### Utilisation d’une instance EC2

👉 Récupérez l’adresse IPv4 publique de l’instance.
Ne confondez pas avec le DNS IPv4 public qui est une adresse web en .com censée rediriger vers votre instance.

👉 Tentez d’exécuter la commande ping sur cette adresse IP.

Rien ne se passe ? C’est tout à fait normal. Par défaut et pour des raisons de sécurité, tous les accès entrant sont bloqués, pour tous les ports et les protocoles (y compris ICMP pour ping).

👉 Modifiez le groupe de sécurité par défaut afin d’autoriser tout le trafic entrant, pour tous les protocoles et à partir de n’importe quelle adresse IP.
Cette modification est évidemment temporaire, les règles seront davantage sécurisées dans le challenge suivant.

👉 À l’aide d’un terminal, connectez-vous au serveur via SSH en spécifiant le chemin vers la clé privée téléchargée précédemment.

Pour ce faire, vous devez trouver le nom de l’utilisateur par défaut créé par AWS lors de la configuration de l’instance et vous assurer que la clé corresponde aux exigences de OpenSSH en matière de permissions.

👉 Une fois connecté au serveur, vérifiez l’utilisateur courant grâce à la commande suivante.

whoami

##### Administration d’une instance EC2

👉 Depuis l’interface de la console EC2, arrêtez complètement l’instance en sélectionnant "Arrêter l’instance" puis démarrez-là de nouveau.

👉 Tentez de vous connecter au serveur via SSH en reprenant la commande que vous avez précédemment exécutée.

Rien ne se passe ? De nouveau, c’est tout à fait normal. Par défaut, lors de la création d’une instance EC2, une adresse IP publique dynamique est attribuée et celle-ci est libérée à chaque arrêt de l’instance.


👉 Trouvez un moyen d’allouer et attribuer un adresse IP publique statique à votre instance via les adresses IP élastiques.

Ce service est inclus dans le prix d’une instance EC2, mais peut être facturé si l’adresse IP commandée n’est pas attribuée ou bien si elle est attachée à une instance arrêtée.

👉 Une fois la nouvelle adresse IP publique statique rattachée à votre instance, tentez de l’utiliser pour vous connecter via SSH.

👉 Pour terminer ce challenge, assurez-vous de résilier et libérer toutes les ressources crées afin d’éviter une surfacturation et de dépasser le tier gratuit d’AWS :

- Adresses IP élastiques : dissociez puis libérez l’adresse IP publique précédemment réservée
- Instances : résiliez (terminate) l’instance "myfirstvps"

#### :bike: Virtual servers with Compute Engine

##### Création d'une instance Compute Engine

Google Compute Engine permet de louer des serveurs virtuels, appelés instances, où vous pouvez héberger des applications web en production.

Dans GCP, les instances sont également liées à des régions et des zones. Sélectionnez la région et la zone la moins chère pour une instance de type "e2-micro" en comparant les prix sur la page de tarification de Google Cloud.

👉 Connectez-vous à la Google Cloud Console.

Allez à "Compute Engine" puis "Instances de VM".
Cliquez sur "Créer une instance".
Nom : myfirstvps
Région et zone : choisissez selon l'étape précédente
Machine type : e2-micro
Boot disk : Sélectionnez Debian GNU/Linux 11 (bullseye) avec 15 Go de disque SSD
Firewall : Cochez les options pour permettre le trafic HTTP et HTTPS.

👉 Dans la section "SSH Keys" de la page de création d'instance, ajoutez une clé publique SSH. Vous devrez générer une paire de clés SSH sur votre machine locale si vous n'en avez pas déjà.

Conservez la clé privée en lieu sûr pour vous connecter à l'instance.

👉 Cliquez sur "Create" pour lancer votre instance. Le déploiement prend généralement quelques secondes.

##### Utilisation d'une instance Compute Engine

👉 Retournez à la liste des instances Compute Engine et notez l'adresse IP externe attribuée à votre instance.

👉 Ouvrez un terminal et connectez-vous à votre instance

##### Administration d'une instance Compute Engine

👉 Dans la Google Cloud Console, sélectionnez votre instance et utilisez les options "Arrêter" puis "Démarrer" pour redémarrer l'instance.

👉 Allez à "VPC network" > "Adresse IP externe" et changez le type de l'adresse IP de votre instance de "Ephémère" à "Statique".

👉 Utilisez la même commande SSH que précédemment avec la nouvelle adresse IP statique.

👉 Supprimez l'instance et libérez l'adresse IP externe réservée pour éviter des frais inutiles.

#### :bike: Virtual servers with Azure VM

##### Création d'une instance Azure VM

Azure Virtual Machines offre la possibilité de déployer des serveurs virtuels pour des applications, y compris en production.

Comme pour AWS et GCP, les prix des services Azure peuvent varier en fonction de la région. Sélectionnez la région la moins chère pour une instance comparable, comme une "B1s" sur la page des prix Azure.

👉 Connectez-vous à Azure Portal et allez dans "Virtual machines" puis cliquez sur "Add".

Choisissez les options suivantes lors de la configuration :

- Subscription: Sélectionnez votre abonnement.

- Resource group: Créez un nouveau groupe de ressources ou en sélectionnez un existant.

- Virtual machine name: myfirstvps

- Region: Sélectionnez selon votre choix précédent.

- Image: Choisissez "Debian 11" pour le système d'exploitation.

- Size: Sélectionnez "Standard B1s".

- Administrator account: Choisissez "SSH public key" et fournissez votre clé publique SSH.

- Public inbound ports: Choisissez "Allow selected ports" et sélectionnez SSH (22), HTTP (80), et HTTPS (443).

👉 Disque et options de réseau :

- Disk options: Choisissez un disque SSD avec une capacité de 15 Go.
- Networking: Sélectionnez un Virtual Network existant ou créez-en un nouveau. Utilisez les paramètres par défaut pour le subnet et la public IP.

👉 Vérifiez et revoyez les options, puis cliquez sur "Review + create" et ensuite sur "Create" pour déployer votre machine virtuelle.

Utilisation de l'instance Azure Virtual Machine

👉 Une fois l'instance déployée, retournez à la page "Virtual machines", sélectionnez votre VM et notez l'adresse IP publique affichée.

👉 Ouvrez un terminal et connectez-vous à votre instance

##### Administration d'une instance Azure VM

👉 Depuis Azure Portal, sélectionnez votre VM, puis utilisez les options "Stop" et "Start" pour redémarrer l'instance.

👉 Allez à "IP addresses" sous les paramètres de la VM et changez le type de l'IP de "Dynamic" à "Static". Réservez l'adresse IP.

👉 Utilisez la même commande SSH que précédemment avec l'adresse IP statique désormais assignée.

👉 Supprimez la VM et libérez l'adresse IP statique pour éviter toute facturation supplémentaire.

#### :bike: Securing your VMs

##### Sécurisation d’une instance EC2

👉 Créez une nouvelle instance nommée "secureme", avec les mêmes caractéristiques que le challenge AWS précédent et en créant une nouvelle paire de clés SSH.
Nul besoin d’assigner cette instance une adresse IP élastique.

👉 Par défaut, le port SSH est ouvert et accessible depuis internet. Trouvez la commande pour vérifier les tentatives de connexion via SSH.

Théoriquement, si vous laissez le serveur SSH avec les paramètres par défaut pendant quelques minutes / heures, vous verrez que des bots tentent de se connecter au serveur même s’il s’agit d’une connexion par clé SSH.

👉 Sécurisez le serveur SSH en désactivant la connexion en tant qu'utilisateur root et en modifiant le port par défaut.

👉 À partir de la console AWS, trouvez l’endroit permettant de configurer le pare-feu en créant un nouveau groupe de sécurité nommé "web-server", basé sur des règles en IPv4 seulement avec les règles entrantes suivantes :

- Ping : IP actuelle seulement
- Nouveau port SSH : IP actuelle seulement ou toutes les IP
- Port HTTP et HTTPS : toutes les IP

👉 Afin de sécuriser davantage le serveur, installez l’application fail2ban qui est chargée de chercher des tentatives répétées de connexions infructueuses dans les logs systèmes et procéder à un bannissement de l’adresse IP incriminée.

##### Sécurisation d’une instance GCE

👉  Créez une instance avec les mêmes caractéristiques que le challenge GCP précédent

👉 Sécurisez le serveur SSH en désactivant la connexion en tant qu'utilisateur root et en modifiant le port par défaut.

👉 À partir de la console, limitez l’accès au serveur avec les mêmes règles que pour l’instance EC2 que vous venez de créer

👉 Installez l’application fail2ban

##### Sécurisation d’une instance Azure VM

👉  Créez une instance avec les mêmes caractéristiques que le challenge Azure précédent

👉 Sécurisez le serveur SSH en désactivant la connexion en tant qu'utilisateur root et en modifiant le port par défaut.

👉 À partir de la console, limitez l’accès au serveur avec les mêmes règles que pour l’instance GCE que vous venez de créer.

👉 Installez l’application fail2ban

##### Vérification de Fail2ban

👉 Vérifiez les logs de fail2ban sur les instances EC2, GCE et Azure VM afin de constater que les intrus éventuels sont bloqués correctement.

##### Suppression des instances

👉 Assurez-vous de résilier et de libérer toutes les ressources crées afin d’éviter une surfacturation et de dépasser le tier gratuit des 3 fournisseurs cloud.

#### :bike: EC2 templating

##### Template d’instance EC2

👉 À partir du tableau de bord EC2, créez un nouveau modèle de lancement nommé "web-server" qui permettra de déployer en un clic une instance paramétrée comme suit :

- Système d’exploitation : Ubuntu Server 20.04, 64 bits (x86)
- Type d’instance : t3.micro
- Paire de clés : Créez une nouvelle clé SSH dédiée à ce modèle
- Paramètres réseau : Sélectionnez le groupe de sécurité créé dans le challenge précédent
- Stockage : 15 Gio

👉 À partir de la section "Détails avancés", trouvez un moyen d’exécuter un script au lancement de l’instance qui devra exécuter les actions suivantes :

- Mise à jour des informations des dépots apt
- Installation du serveur web nginx via apt
- Modification de la configuration de nginx pour cacher le numéro de version dans le header de réponse
- Redémarrer le serveur web afin d’appliquer les modifications

👉 Déployez une instance à partir du modèle créé précédemment.

👉 Après quelques minutes, récupérez l’adresse IP publique de l’instance et vérifiez que le serveur web est prêt et que le reverse proxy a bien été configuré.

curl -v http://XXX.XXX.XXX.XXX

👉 Assurez-vous de résilier et libérer toutes les ressources crées afin d’éviter une surfacturation et de dépasser le tier gratuit d’AWS :

Instances : résiliez (terminate) l’instance "web-server"

#### :bike: Your first client: QuickStart Web Solutions

##### Contexte

Objectif : Cet exercice a pour but de vous initier à la conception d'un schéma d'infrastructure réseau simple pour des machines virtuelles réparties sur plusieurs fournisseurs de cloud (multicloud). L'objectif est de créer un diagramme représentant l'infrastructure de VM pour une petite entreprise, en utilisant uniquement des concepts de base tels que les VM, les sous-réseaux, et les groupes de sécurité.

Entreprise : QuickStart Web Solutions

Secteur d'activité : Développement web et hébergement

Besoins :

- Héberger plusieurs sites web statiques pour leurs clients
- Facilité de gestion et maintenance minimale
- Coûts d'infrastructure réduits

Contraintes :

- Aucune configuration avancée comme les VPNs ou le load balancing
- Maintenir une séparation claire entre les environnements de production et de développement

##### Instructions

👉 Choix des fournisseurs de cloud :

Sélectionnez deux fournisseurs parmi AWS, Google Cloud et Azure.
Expliquez brièvement pourquoi vous avez choisi ces deux fournisseurs pour QuickStart Web Solutions.

👉 Schéma de l'infrastructure :

Répartition des VM : Planifiez comment les VM seront réparties entre les deux clouds. Par exemple, placez les environnements de production chez un fournisseur et les environnements de développement chez un autre, ou distribuez-les en fonction de la spécificité régionale ou de la tarification.

👉 Configuration des réseaux :

Créez des sous-réseaux pour chaque groupe de VM dans chaque cloud. Assurez-vous que chaque sous-réseau est isolé pour sécuriser les environnements de développement et de production.

Assignez des groupes de sécurité pour contrôler l'accès aux VM. Les règles doivent être simples, permettant uniquement le trafic HTTP et SSH.

👉 Simplicité et efficacité : Assurez-vous que le plan est simple et ne nécessite pas de compétences avancées pour être mis en œuvre ou maintenu.

👉 Création du Diagramme :

Utilisez un outil de diagramme comme Microsoft Visio, Google Drawings, ou un logiciel similaire pour créer un schéma visuel de l'infrastructure réseau proposée.

Le diagramme doit inclure les éléments suivants : fournisseurs de cloud, VM, sous-réseaux, et groupes de sécurité. Labellez chaque composant clairement.

##### Livrable

**Diagramme d'Infrastructure Réseau** : Un diagramme clair et bien organisé montrant la répartition des VM et la configuration réseau entre les fournisseurs de cloud sélectionnés.
