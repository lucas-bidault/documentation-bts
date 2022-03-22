---
title: SP10 - Documentation Docker
author: Lucas Bidault
date: 13/12/2021
version: 1
---

# Documentation Docker

[TOC]

## Définition.

- **Docker** : Docker est un service qui permet d’empaqueter une application et ses dépendances dans des conteneurs isolés.

- **Conteneur** : Un conteneur permet d’isoler chaque service (Serveur WEB, Géostationnaire de base de données, application web, …) avec toute leur dépendance. Chaque conteneur peut être relié aux autres par des réseaux virtuels.

## Installation de docker sur Debian.

*Basé sur [Install Docker Engine on Debian | Docker Documentation](https://docs.docker.com/engine/install/debian/)*

### Pré-requis pour l’installation de docker

  Exigences du système d'exploitation : 
  • Debian 11 (stable)
  • Debian 10 (oldstable)

  Si une installation de docker existe, désinstaller-la :

```shell
sudo apt remove docker docker-engine docker.io containerd runc
```

  Installation du module SSL pour apt :

```shell
sudo apt update
sudo apt install ca-certificates curl gnupg lsb-release
```

### Installation du repository

  Ajout de la clef GPG du repository docker :

```shell
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

  Ajout du repository dans la liste des repository APT « /etc/apt/sources.list.d/ » :

```shell
echo \ 
"deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian \
$(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

  Vous pouvez effectuer un sudo apt update afin de voir si la connexion au repository de docker s’est effectuée.

```shell
sudo apt update
[...]
Réception de :5 https://download.docker.com/linux/debian bullseye/stable amd64 Packages [6 092 B]
[...]
```

### Installation de docker

  Maintenant que le repository de docker a été ajouté à la liste d’APT, vous pouvez installer docker :

```shell
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
```

### Test de l'installation de docker

  Afin de tester le fonctionnement de docker, utilisez le conteneur « hello-world » :

```shell
sudo docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
2db29710123e: Pull complete
Digest:
sha256:cc15c5b292d8525effc0f89cb299f1804f3a725c8d05e158653a563f15e4f685
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working
correctly.
```

## Commandes utile pour la gestion des conteneur.

- Docker run : Docker run permet de créer un conteneur et de lancer l’application.
  
  ```shell
  sudo docker run –name (nom pour le conteneur) -p PortHost:PortConteneur (permet le port forwarding du conteneur) [Image du conteneur] [commande]
  ```

- Docker PS : Docker PS permet de montrer l’état des conteneurs installés sur la machine.
  
  ```shell
  sudo docker ps
  
  CONTAINER    ID    IMAGE    COMMAND
  [...]           nginx    "/docker-entrypoint...."
  
  CREATED            STATUS                            PORTS
  2 seconds ago        Up 1 second        0.0.0.0:8080->80/tcp, :::8080->80/tcp
  ```

- Docker start : Docker start permet de démarrer un conteneur.
  
  ```shell
  sudo docker start [ID du conteneur]
  ```

- Docker stop : Docker start permet l’arrêt d’un conteneur.
  
  ```shell
  sudo docker stop [ID du conteneur]
  ```

- Docker exec : Docker exec permet d’exécuter une application dans le conteneur.
  
  ```shell
  sudo docker exec -u [Utilisateur] -it(intégration du cli) [Nom/ID duconteneur] [Commande]
  ```
