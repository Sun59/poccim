# Poc des connaissances Devops

L'idée de ce POC à pour but de tester les compétences devops d'un collaborateur cette documentation à pour but d'évoluer au fur et a mesur de l'apprentissage

## Commandes utilisées pendant le projet

* `brew install python` - Create a new project.
* `pipenv lock` - Start the live-reloading docs server.
* `pipenv sync --dev` - Build the documentation site.
* `pipenv shell` -
* `pipenv run serve` -
* `mkdocs new madoc` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs -h` - Print help message and exit.

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
 
 * `https://gitlab.com/hammouti.samir/poc/-/blob/master/ubuntu/Vagrantfile`

il nous reste qu'a lancer notre fichier Vagrantfile

* `vagrant up`

* `vagrant ssh` pour se connecter à la vm créé 


Un Vagrantfile par dossier 






* `Si vous voulez crée une 2eme VM avec une autre box ou la même il faut créer un nouveau répertoire et reproduire l'opération`



## Ansible

	### Introduction:
	
	Brew install ansible
	
	
(pyp3env-ansible) samirhammouti@MacBook-Pro-de-samir ubuntu % ansible --version

* `ansible 2.10.5
  config file = /Users/samirhammouti/Projet/ubuntu/ansible.cfg
  configured module search path = ['/Users/samirhammouti/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/local/Cellar/ansible/2.10.6/libexec/lib/python3.9/site-packages/ansible
  executable location = /usr/local/bin/ansible
  python version = 3.9.1 (default, Feb  1 2021, 20:42:01) [Clang 12.0.0 (clang-1200.0.32.29)]`
  
  


	### Playbook:
Création de mon playbook d'install apache2 sur ma box ubuntu

Je crée un playbook générique qui pourra servire à d'autre installation autre qu'apache

un playbook s'écrit en yaml et nous l'appellerons provision-playbook.yml
--- 
- 
  name: "installation"
  become: true
  hosts: all
  user: vagrant
  roles: 
    - 
      role: apache
      
 
 * `name: "installation"` - Nom.
* `become: true` - bonne question.
* ` hosts: all` - ce refere à notre fichier hosts là nous utilison all pour ciblé tout le fichier mais nous pourrons être plus précis sur un group de server.
* `user: vagrant` - c'est l'utilisateur qui va ce connecter à la VM
* `roles:` - nous permettra d'affiner nos action 
* ` - 
    role: apache` - ansible-galaxy apache pour nous générés une architecture de fichier .
      
   Tree
   
    └── apache
    ├── README.md
    ├── defaults
    │   └── main.yml
    ├── files
    ├── handlers
    │   └── main.yml
    ├── meta
    │   └── main.yml
    ├── tasks
    │   └── main.yml
    ├── templates
    │   └── apache.conf.j2
    ├── tests
    │   ├── hosts
    │   ├── inventory
    │   └── test.yml
    └── vars
        └── main.yml
 
      
	### Role:
Une fois notre archi télécharger via ansible-galaxy nous allons pouvoir parametrer nos actions (tasks)

├── tasks
    │   └── main.yml
---
# tasks file for apache
    - name: install apache2
      apt: name=apache2 update_cache=yes state=latest
      
    - name: "Create docuement root"
      file:
          path: "/var/www/{{ ap_http_host_dir }}"
          state: directory
     
    - name: "Copy source html"
      copy:
         src: "/Users/samirhammouti/Projet/projet/site"
         dest: "/var/www/{{ ap_http_host_dir }}"  
	
	
### Handelers:
##handlers recensera les événements Ansible liés à des rôles pour nous apache

---
(# handlers file for apache)
  
  - 
    name: "restart apache2"
    service: "name=apache2 state=restarted"

## Docker

J'ai créé qu'un fichier Dockerfiles
l'idée était de crée un fichier Dockerfiles avec une distrib alpine 3.13 et y faire tourner notre site 


##Git

Créer un compte gitlab 
Créer un nouveau projet 

git config --global user.name "K2 Sunshine" (K2 2eme plus grand sommet du monde)
git config --global user.email "hammouti.samir@gmail.com"
 
on se met à la racine du dossier qu'on veut push

* `cd /Users/samirhammouti/Projet`
	
* `git init`
* `git remote add origin https://gitlab.com/hammouti.samir/poc.git`

* `git add .`
* `git commit -m "commentaire"`
* `git push -u origin master`

* `https://gitlab.com/hammouti.samir/poc`

Si vous avez mis à jour le fichier sur votre poste et que vous voulez renvoyer les informations au repo git
* `git add .`
* `git commit -m "commentaire"`
* `git push`


##Conclusion 

* `Créer une documentation avec mkdocs` - Ok.
* `réation d’une machine virtuelle` - Ok.
* `Ecrire le playbook de provisionnement` - Le plus compliqué dans le playbook de provisionnement c'était de faire la part des choses entre Ansible / Vagrant / Ma machine et ma VM
des problèmes de connexion SSH notement par rapport à l'utilisateur qui se connecter (vagrant)
pour le playbook de provisionement j'ai simplement copier mon home vers la vm  ça répondé une partie à la question je pense.
* `Ecriture des tests d’un rôle apache` - C'était assez compliqué, la notion de rôles a été très compliqué à assimiler. entre playbook et rôles je ne comprenais pas. j'ai malgré tout une notion beaucoup plus claire et l'étendu de la fonctionnalité une fois maitrisé. j'ai réussi à crée un role d'installation apache
* `Ecrire un playbook utilisant le rôle apache` - J'ai compris beaucoup trop tard pour commencer à produire quelques choses de viable.
* `Ecrire un Dockerfile` - Lors de mon PT j'ai eu du mal à comprendre la cohabitation entre mon Mac OS / Homebrew / et Pipenv lors du building de mon Dockerfiles pour le test j'ai des errreurs de dépendance. (j'étais pas dans mon pipenv) 
.


Je n'ai vraiment pas l'habitude de rédiger des procédures sous cette formes.



