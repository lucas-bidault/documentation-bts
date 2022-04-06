---
title: SP16-M1 ~ Installation de gitlab
author: Lucas Bidault
date: 07/03/2022
version: 1
---

# SP16-M1 ~ Installation de gitlab

[TOC]

> :warning: La documentation est uniquement valable pour fedora (ou autre distribution RHEL).

```
webadmin: https://172.16.56.200:9090/
username: gitlabadmin
password: Etudiant_007
```

## Installation et configuration des dépendances

```shell
sudo dnf install postfix
```

```shell
sudo systemctl enable postfix
sudo systemctl start postfix
```

## Installation et configuration de gitlab ce

```
web : http://172.16.56.200/
password : root
password : Etudiant_007
```

### Installation de gitlab

```shell
cd /tmp/
wget --content-disposition https://packages.gitlab.com/gitlab/gitlab-ce/packages/el/8/gitlab-ce-14.6.6-ce.0.el8.x86_64.rpm/download.rpm
```

```shell
cd /tmp/
sudo rpm -Uvh gitlab-ce-14.6.6-ce.0.el8.x86_64.rpm
```

### configuration de gitlab

```shell
sudo gitlab-ctl reconfigure && sudo gitlab-ctl restart
```

### Changement du mot de pass root

```shell
sudo gitlab-rake "gitlab:password:reset[root]"
```

### Création d'un utilisateur pour la mairie

Connectez vous avec le compte `root` sur gitlab.
Allez dans le menu `Overview > Users`, puis cliquez sur `New user`.

```
Name        : SCA Administration Système
Username    : sca-sysadmin
Email       : sca-admin@sca.lan
```

> :warning: N'oubliez pas le `Validate user account` dans la catégorie `Access`.

Maintenant, cliquez sur `Create user`.
Enfin, modifier le mot de pass de l'utilisateur en utilisant la commande `sudo gitlab-rake "gitlab:password:reset[sca-sysadmin]"`.

### Création d'un projet pour les script ansible de la mairie.

Connectez vous sur le compte `sca-sysadmin`, puis créer un nouveau projet en cliquant sur `Create new project > Create blank project`.
Nommez-le `playbook-mairie`, et mettez la visibilité sur `Private` afin que seul les utilisateur choisis puissent accédés au projet.
