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
