# Vagrant

	### Introduction: Vagrant est un des outils en ligne de commande qui permet de virtualiser rapidement des machines en utilisant la plupart des hyperviseurs comme HyperV, Libvirt, Parallels, VMWare et VirtualBox. 
	 Dans mon cas je vais devoir passer par homebrew pour l'installation.	
	
	### Installation:
	
* `brew cask install virtualbox` 
* `brew cask install vagrant` 


##il va falloir ajouter quelques plugin 

vagrant plugin list

* `vagrant-hostsupdater (1.2.1, global)
vagrant-vbguest (0.28.0, global)
  - Version Constraint: 0.28
vagrant-vbox-snapshot (0.0.10, global)`

Une fois que vagrant est opérationnel il va falloir lui attribué un OS qu'on appel box.

* `vagrant box add ubuntu(nombox) https://app.vagrantup.com/ubuntu/boxes/trusty64/versions/20190514.0.0/providers/virtualbox.box
si vous avez besoin d'ajouter une autre box il suffiera dans changer l'url par l'url de la nouvel box` 

vagrant box list 

* `(pyp3env-ansible) samirhammouti@MacBook-Pro-de-samir ubuntu % vagrant box list                      
centos/8        (virtualbox, 2011.0)
oraclelinux/8   (virtualbox, 8.3.182)
ubuntu/bionic64 (virtualbox, 20210129.0.0)
ubuntu2         (virtualbox, 0)` 

Il nous reste plus qu'a Initier le fichier de configuration Vagrant 

vagrant init (nomdelabox)
vagrant init ubuntu2

A `Vagrantfile` has been placed in this directory. You are now
ready to `vagrant up` your first virtual environment! Please read
the comments in the Vagrantfile as well as documentation on
`vagrantup.com` for more information on using Vagrant.

ils nous reste plus qu'a parametrer notre fichier Vagrantfile
vi Vagrantfile 

Ce fichier de configuration va nous permettre de :
Choisir un hostname /cpu/ram///... à nous d'ajouter les informations voulu

configuration par defaut : 

* `vagrant.configure("2") do |config|
 config.vm.box = "ubuntu2"`
 
 configuration personnalisé : 
 
 [Vagrantfile](https://gitlab.com/hammouti.samir/poc/-/blob/master/ubuntu/Vagrantfile)

il nous reste qu'a lancer notre fichier Vagrantfile

* `vagrant up`

* `vagrant ssh` pour se connecter à la vm créé 


Un Vagrantfile par dossier 






* `Si vous voulez crée une 2eme VM avec une autre box ou la même il faut créer un nouveau répertoire et reproduire l'opération`

