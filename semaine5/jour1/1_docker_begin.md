**Formation devOps**
_La capsule - Batch Juin-Août 2024_

:fire: Exercices et corrections formation devOps :fire:

---

**Semaine 5**

**Jour 1 : Conteneurisation**

---

# 1 - DOCKER BEGIN

## <ins> Installer docker et dépendences sur UNBUNTU </ins>
(il faut installer depuis le "repo docker dédié ubuntu" et non le "répo officiel de ubuntu")
  
- set repo :
```
sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
```
  
- Check répo Docker vs répo Ubuntu avant install :

```
apt-cache policy docker-ce
```
> _url sont celle de Docker et non ubuntu_
  
- Installer Docker
```
sudo apt install docker-ce
```

- Checker que Docker tourne
```
sudo systemctl status docker
```

* **Pour ne pas à avoir a SUDO chaque fois**  
On ajoute le groupe et on se delog/relog
```
sudo usermod -aG docker ${USER}
su - ${USER}
```
