---
title: SP0 - INTRODUCTION - Documentation TrueNas
author: Lucas Bidault
date: 03/10/2021
version: 1
---

# SP0 - INTRODUCTION - Documentation TrueNas



[TOC]



## Installation de TrueNas

Pour installer TrueNAS, je vais utiliser l’ISO de TrueNAS-12. Après le démarrage de l’ISO un menu avec plusieurs choix s’ouvrira.

<img src="assets/2022-03-16-14-46-24-image.png" title="" alt="" data-align="center">

Je choisis l’option « Install/Upgrade » afin d’installer TrueNAS sur le disque de la machine.

Ensuite l’installateur me demandera quel disque choisir pour TrueNAS.

<img title="" src="assets/2022-03-16-14-48-25-image.png" alt="" data-align="center">

Je choisis le disque « da0 » de 8Go pour le système TrueNAS.

L’installeur partitionnera automatiquement le disque « da0 » pour le système TrueNAS.

Après l'installation du système l’installeur de TrueNAS demande de choisir entre UEFI et BIOS. 

Ici la configuration de démarrage de la machine virtuelle est « Legacy BIOS », alors je choisis « Boot via BIOS ».

<img title="" src="assets/2022-03-16-14-48-44-image.png" alt="" data-align="center">

Maintenant l’installation de TrueNAS est terminé, je peux redémarrer la machine.

## Configuration de TrueNas

### Configuration Réseau.

Pour configurer le réseau, je choisis l’option « 1 » du menu.

J’utilise la configuration réseau suivante :
DHCP : NON
NOM  : vtnet0
IPv4 : 172.16.55.20 / 24
IPv6 : NON

<img title="" src="assets/2022-03-16-14-49-03-image.png" alt="" data-align="center">

Après la configuration du réseau, je vais paramétrer la route par défaut, ici 172.16.55.253.

<img src="assets/2022-03-16-14-49-14-image.png" title="" alt="" data-align="center">

### Configuration du RAID-5

Pour configurer le raid-5, je vais utiliser le raid-z de TrueNAS qui est un équivalent au raid-5.
Je me connecte sur la page web de TrueNAS : http://172.16.55.20/.
Sur le menu de gauche je vais sur « Storage > Pools » puis « add » pour rajouter un groupe de disque.

![](assets/2022-03-16-14-50-07-image.png)

Ensuite je choisis le nom de ma « Pool », ici ce sera « RAID ».

![](assets/2022-03-16-14-50-58-image.png)
