# lab-vagrant-nginx

- [Installation du lab](#installation-du-lab)
- [Déploiement VMs](#déploiement-vms)
- [Déploiement multiples](#déploiement-multiples)
- [Pour aller plus loin](#pour-aller-plus-loin)

## Installation du lab

### VirtualBox
par un dépot 
```
apt install virtualbox 7.0
```

par le paquet au préalable téléchargé
```
sudo dpkg -i nom_du_paquet.deb
```
=> si problème lors du chargement dans le kernel de vb, installer le paquet 
```
sudo apt install linux-headers-$(uname -r) dkms
```

### Vagrant: installation
```
sudo apt install vagrant
```
ou pour avoir la dernière version:
https://developer.hashicorp.com/vagrant/downloads

## Déploiement VMs
Déploiement depuis le Cloud Vagrant: informations indiquées sur l'image concernées,
exemple:https://app.vagrantup.com/generic/boxes/debian10

OU déploiement local, téléchargement de l'ISO:
https://app.vagrantup.com/generic/boxes/debian10
(renommer l'image téléchargée en debian10.box)

Déploiment local
```
vagrant box add debian10 /path/to/image.box
vagrant init debian10
```
On liste les images
```
vagrant box list
```
Depuis le répertoire files du repo git:
Copier le contenu du Vagrantfile dans celui qui vient d'être créé

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

## Déploiement multiples
Au lieu de copier le Vagrantfile du repo, copiez le contenu de
Vagrantfile_liste

Celui ci liste chaque VM, et peut être personnalisé (différentes options selon les VMs)

Pour lister les vms actives sous virtualbox:
```
VBoxManage list runningvms
```
Pour se connecter en ssh:
```
vagrant ssh nom_vm
```

sinon possibilité de cibler les ports indiqués pour chaque vms (ici 2200, 2201, 2202)
pour cibler une machine:
```
ssh -p 2202 vagrant@localhost
(mdp vagrant)
```

Arrêt / suppression VMs
```
sudo vagrant halt nom_vm
sudo vagrant destroy nom_vm
```

## Pour aller plus loin

### Paramétrer une page d'accueil par serveur:

=> le fait de déposer un fichier dans le répertoire courant (le même ou se trouve le Vagrantfile) il sera automatique disponible sous la VM sous le répertoire /vagrant

```
touch index.html (puis on y insère le contenu souhaité)
```
Et dans le Vagrantfile, rajoutez lors du déploiement des scripts:

```
 # déploiement de l'index, exemple site 1   
    config.vm.provision "shell", inline: <<-SHELL
        rm /etc/nginx/sites-enable/*
        cp /vagrant/index.html /etc/nginx/sites-enable/
        sed -i 's/site/site1/g' /etc/nginx/sites-enable/index.html 
        service nginx restart
    SHELL
```

Permettre un espace d'échange entre la machine hôte et les vms:


```
config.vm.synced_folder ".", "/var/tmp"

```
