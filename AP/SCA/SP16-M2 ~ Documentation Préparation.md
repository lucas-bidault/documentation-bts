---
title: SP16-M2 ~ Préparation de l'environnement de travail
author: Lucas Bidault
date: 28/03/2022
version: 2
---

# SP16-M2 ~ Préparation de l'environnement de travail

[TOC]

## Installation des dépendances

Installation des diférentes dépendances pour le projet

### Installation de git

Git est un outils qui permet

```shell
sudo dnf install git 
```

### Installation de Python 3

Python va nous ...

```shell
sudo dnf install python3 python3-pip
```

### Installation de virtualenv

... le but des virtualenv

```shell
pip3 install virtualenv
```

## Création d'un projet git

... Explique git

### Création d'un nouveau projet avec GitHub

... Explique le but

Connectez vous sur github afin de crée un nouveau répo.

Pour se projet le répo sera appelé 'playbook-mairie'

### Copie du projet dans le répertoire du poste admin

```shell
git clone http://172.16.56.200/sca-sysadmin/playbook-mairie.git
```

Maintenant vous pouvez ouvrir le répertoire avec visual studio code.

### Configuration de git

Configuration de nom d'utilisateur

```shell
git config user.name "sca-sysadmin"
```

Configuration du mail

```shell
git config user.email "your_email_address@example.com"
```

## virtualenv

### Creation du virtualenv

```shell
virtualenv venv -p python3
```

```shell
source venv/bin/activate
```

### Installation des modules

```shell
pip3 install ansible
```
