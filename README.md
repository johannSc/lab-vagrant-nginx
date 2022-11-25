# lab-vagrant-nginx

- [Installation du lab](#installation-du-lab)
- [Déploiement VMs](#déploiement-vms)
- [Déploiement multiples](#déploiement-multiples)

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
Depuis le répertoire files du repo git:
Copier le deploy.sh dans le répertoire courant

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
Vagrantfile_boucle
ou
Vagrantfile_liste

Les deux effectues les mêmes actions
- Le premier est une boucle qui appel le nombres de VMs demandées
- Le second est une liste de chaque VM, plus long mais peut être personnalisé (différentes options selon les VMs)
