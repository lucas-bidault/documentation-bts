---
title: SP6 - Documentation OpenSense
author: Lucas Bidault
date: 29/11/2021
version: 1
---

# SP6 - Documentation OpenSense

[TOC]

## Installation d'OpenSense

Pour installer OpenSense. J'ai utiliser une machine virtuelle avec la configuration suivante:

- HDD  : 128 Go

- vCPU : 2

- RAM  : 8 Go

- NET  : Vlan 56 et 52

Pour l'installation, je démarre sur le CD, puis je me connecte avec l'utilisateur `root` et le mot de passe `opensense`

<img title="" src="assets/4a166fabdbc8f7e5374434ae7c0062bb8f9cb808.png" alt="" data-align="center">

Ensuite, je sélectionne l'option `8` sur le menu. Ensuite j'entre la commande `opnsense-installer`

<img src="assets/3e6338cd960fb5d68b8b96a1fedc87d973903a0d.png" title="" alt="" data-align="center">

Maintenant que l'installation est lancer, je vais choisir `install (UFS)` dans le menu.

<img src="assets/d6792f974ba2332e8bf574aa2e65cc909ae28045.png" title="" alt="" data-align="center">

Ensuite, il faut choisir le disque pour l'installation, ici ce sera `ada0`.

<img src="assets/50f8c39dbeded0fc02cca0e1dfc243de946fa492.png" title="" alt="" data-align="center">

Après l'installation du système, l'installateur nous demande de changer le mot de passe de l'utilisateur `root`.

<img src="assets/18081f85d434426db907962b77fa4d4d1ed8ce94.png" title="" alt="" data-align="center">

## Configuration d'OpenSense

### Ajout de la règle OpenVPN

Afin de faire fonctionner OpenVPN il faut autoriser le WAN a accéder au port 1194.
Pour se faire il faut aller sur le menu de droite. Dans l’onglet `Pare-feu > Règles > WAN`.

<img src="assets/91481960e12b083db9e7144b09f3d4f2cc4c44bc.png" title="" alt="" data-align="center">

<img src="assets/16de01f85aca6d67bf61dd29db142e019cb43b69.png" title="" alt="" data-align="center">

<img src="assets/24f25eb315455139436a6f194812782456c6b7c9.png" title="" alt="" data-align="center">

### Configuration du proxy

<img src="assets/e4ac065b1a88a80ecf82362af20b833f7bcfd015.png" title="" alt="" data-align="center">

<img src="assets/d56a6ea0e56b46787f985d73a6fca18f8b016a77.png" title="" alt="" data-align="center">

<img src="assets/911d8d43070ca538c138dcee143790084d5c122f.png" title="" alt="" data-align="center">
