---
title: SP16-M3 ~ Création de l'inventaire
author: Lucas Bidault
date: 28/03/2022
version: 1
---

# SP16-M3 ~ Création de l'inventaire

[TOC]

## Création de l'architecture pour l'inventaire

*Documentation basé sur [Best Practices Ansible Documentation](https://docs.ansible.com/ansible/2.8/user_guide/playbooks_best_practices.html)*

Ici nous allons séparé les serveurs de production et staging (Pré-production).

Exemple :

```
inventories/
└─ production/
   ├─ hosts               # Fichier d'inventaire des serveur de production
   ├─ group_vars/
   │  ├─ group1.yml       # Assination des variable pour un groupe particulier
   │  └─ group2.yml
   └─ host_vars/
      ├─ hostname1.yml    # Assination des variable pour un hôte particulier
      └─ hostname2.yml

inventories/
└─ staging/
   ├─ hosts               # Fichier d'inventaire des serveur de pré-production
   ├─ group_vars/
   │  ├─ group1.yml       # Assination des variable pour un groupe particulier
   │  └─ group2.yml
   └─ host_vars/
      ├─ hostname1.yml    # Assination des variable pour un hôte particulier
      └─ hostname2.yml
```

Voici la structure de notre inventaire ansible :

```
inventories/
├── production
│   └── hosts
└── staging
    └── hosts
```

## Ajout des hôte dans le fichier hosts

Nous pouvons a présent rajouter nos hôtes dans le ficher `inventories/productio/hosts`. Cette configuration est utile quand le serveur possède pas la clé public ssh de notre ordinateur.

```
[serveur_gitlab]
172.16.56.200 ansible_connection=ssh ansible_ssh_user=gitlabadmin
```

```
[serveur_gitlab]               # On definit le groupe de notre machine
172.16.56.200                  # Domaine ou addressse IP du serveur     
ansible_connection=ssh         # Choix du protocole de connexion 
ansible_ssh_user=gitlabadmin   # Nom d'utilisateur du serveur
```

Cependant il est préférable d'utiliser une authentification par clé ssh.

1. Création de la clé ssh sur notre poste
   
   ```shell
   ssh-keygen -a 128 -t ed25519 -C "Poste Admin"
   ```

2. Maintenant on transfert notre clé public ssh sur le serveur.
   
   ```shell
   ssh-copy-id gitlabadmin@172.16.56.200
   /usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
   /usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
   gitlabadmin@172.16.56.200's password: 
   
   Number of key(s) added: 1
   
   Now try logging into the machine, with:   "ssh 'gitlabadmin@172.16.56.200'"
   and check to make sure that only the key(s) you wanted were added.
   ```

3. Modification des paramètres de l'hôte qui sont a présent inutil.
   
   ```diff
   - 172.16.56.200 ansible_connection=ssh ansible_ssh_user=gitlabadmin ansible_ssh_pass=Etudiant_007
   + 172.16.56.200 
   ```

## Test du fichier hosts

Afin de tester la configuration de l'hôte ajouter dans l'inventaire, nous allons exécuter la command Ad-Hoc `Ping`.

```shell
ansible -i inventories/production/hosts -m ping serveur_gitlab
```

```json
172.16.56.200 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```
