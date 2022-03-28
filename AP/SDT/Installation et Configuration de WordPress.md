---
title: Documentation - Installation et Configuration de WordPress
author: Lucas Bidault
date: 18/09/20
version: 2
---

# Installation et Configuration de WordPress

[TOC]

## Prérequis

- Un poste client

- Un poste serveur

- XAMPP 3.2.4 :
  
  - MariaDB 10.3.15
  
  - Apache 2.4.39
  
  - PHP 7.3.6
  
  - phpMyAdmin 4.9.0.1

## Installation et Configuration de XAMPP

1. Tout d'abord installez XAMPP https://www.apachefriends.org/fr/download.html, ensuite ouvrez le `Control Panel` XAMPP.
   
   <img src="file:///home/yutetsudo/.config/marktext/images/2022-03-24-19-38-14-image.png" title="" alt="" data-align="center">

> On peut voir que les services Apache et MySQL sont activés.

2. Après, il faut configurer la base de données. Connectez vous http://localhost/phpmyadmin/

<img src="file:///home/yutetsudo/.config/marktext/images/2022-03-24-19-40-31-image.png" title="" alt="" data-align="center">

> Sur `phpMyAdmin`, cliquez sur `Nouvelle base de données` et nommez là `startdev_wordpress`. 

## Installation de WordPress

Pour installer WordPress 5.5.1, il faut aller sur le site http://fr.wordpress.org/.

<img src="assets/2022-03-24-19-45-44-image.png" title="" alt="" data-align="center">

Ensuite, cliquez sur `Télécharger WordPress 5.5.1` afin de télécharger le fichier ZIP puis dé-zipper le fichier dans `C:\XAMPP\HTDOCS\`.

<img src="assets/2022-03-24-19-47-29-image.png" title="" alt="" data-align="center">

## Configuration de WordPress

Connectez vous à l'adresse http://localhost/wordpress/, sur la page de configuration rentrez les informations de la base de données configurée précédemment.

<img src="assets/2022-03-24-19-49-51-image.png" title="" alt="" data-align="center">

Maintenant, indiquez toutes informations nécessaires comme : (Titre du site, Identifiant et Mot de passe ainsi que la messagerie du propriétaire).

<img src="assets/2022-03-24-19-51-48-image.png" title="" alt="" data-align="center">

Maintenant que WordPress est installé, vous pouvez vous connecter sur http://localhost/wordpress/.

<img src="assets/2022-03-24-19-53-17-image.png" title="" alt="" data-align="center">
