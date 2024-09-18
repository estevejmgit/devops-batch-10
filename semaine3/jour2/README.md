# Formation devOps

:pill: La capsule

:fire:  Documentation d'accompagnement au cycle devOps :fire:

---

## Semaine 3 :zap:

Versionning avancé avec Git, Jira et intégration continue et tests d'intégration

### Jour 2 : Le ticketing avec Jira

:warning: Difficulté avec le connection JIRA - GitLab

- Temps de latenece entre gitlab et jira sur l'action du commit
- Autmoation liées aux issues : Différence issues / Tickets il faut bien créer une "issue" dans JIRA et ne passer par la création de ticket sur le Board Jira

:information_source: De manière globale, les menu de navigation de Jira changent régulièrement   : il faut bien comprendre la segmentation des responsabilités : 

- users au niveau organisation
- users au niveau projet
- users dans des équipes

selon le contexte et les droits accordé, il faut parfois inviter les users à l’organisation ou le projet avant de pouvoir les intégrer à des équipes

Sur la connection Jira - gitlab : bien comprendre que c’est le namespace [user ou group gitlab] de gitlab qu’on connecte au Jira

L'important c'est de comprendre que le lien se fait en connectant JIRA et Gitlab , DEPUIS JIRA (app JIRA-gitlab)
qu'ensuite il faut choisir dans "JIRA > app > Gitlab" le bon namespace utilisé sur gitlab (qui peut être un nom de user ou un groupe gitlab) 

gitlab.com:**namespace**/project

et qu'à partir de là on peut synchroniser les actions à travers les "automations gitlab" (ou les mot-clef "now #done" dans les messages commit, avec l' id/clef d'un Ticket si on veut) 

#### :bike: GitLab ticketing

##### Création d’un milestone

##### Création de tickets

##### Service Desk

#### :bike: Exploring Jira

##### Création d’un projet Kanban

##### Ajout de tickets

##### Jira Query Language (JQL)

#### :bike: Jira meets GitLab

##### Setup J&G

##### Intégration de GitLab sur Jira

##### Lier un commit sur GitLab à un ticket Jira

##### Merge request et changement de statut du ticket

#### :bike: Jira automation

##### Setup Automation

##### Déclencheur et conditions

##### Smart Values

##### DevOps Automation

##### Audit Log

#### :bike: Jira scripting

##### Connexion à l’API REST de Jira

##### Bash scripting

##### Afficher des données

##### Récupérer des tickets avec JQL
