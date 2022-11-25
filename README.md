# lab-vagrant-nginx

- [Installation du lab](#installation-du-lab)
- [Déploiement VMs](#déploiement-vms)

## Installation du lab

### VirtualBox
par un dépot 
```
apt install virtualbox 7.0
```

par le paquet au préalable téléchargé
```
dpkg -i nom_du_paquet.deb
```
=> si problème lors du chargement dans le kernel de vb, installer le paquet 
```
sudo apt install linux-headers-$(uname -r) dkms
```

### Vagrant: installation
```
apt install vagrant
```
Copier les fichiers nécessaires pour le tp présents dans le répertoire files du repo git
```
cp deploy.sh
cp Vagrantfile
```

## Déploiement VMs

Téléchargement de l'ISO:
https://app.vagrantup.com/generic/boxes/debian10

Déploiment local
```
vagrant box debian10 /path/to/image.box
vagrant init debian10
```
On liste les images
```
vagrant box list
```
Modification du Vagrantfile selon

Lancement de la machine virtuelle:
```
sudo vagrant up
```

puis connexion à la VM:
```
sudo vagrant ssh
```

Vérification du déploiement de Nginx:
```
wget -qO- localhost
```
