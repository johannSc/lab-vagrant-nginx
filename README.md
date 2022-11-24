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

```
touch Vagrantfile
```
Y intégrer le contenu du Vagrantfile présent sous le repo
```

touch deploy.sh
```
Y intégrer le contenu du deploy.sh présent sous le repo
```

## Déploiement VMs
Lancement de la machine virtuelle:
```
sudo vagrant up --provider virtualbox
```
puis connexion à la VM
```
vagrant ssh
```
Vérification du déploiement de Nginx:
```
wget -qO- localhost
```
Si souhaité, ajout au Vagrant file du portforwarding de la VM; config.vm.network "forwarded_port", guest: 80, host: 8080, id: "nginx"
