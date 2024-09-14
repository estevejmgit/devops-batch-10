# Formation devOps

:pill: La capsule

:fire:  Documentation d'accompagnement au cycle devOps :fire:

---

**Semaine 5**

**Jour 1 : Conteneurisation**

---

# 1 - DOCKER BEGIN

## Installer docker et dépendences sur DEBIAN

Les Virtual Machines des élèves étant sur pve proxmox,il faut suivre la [doc d'install 
correspondante] (https://docs.docker.com/engine/install/debian/)


* **Pour ne pas à avoir a SUDO chaque fois**  
On ajoute le groupe et on se delog/relog
```
sudo usermod -aG docker ${USER}
su - ${USER}
```
