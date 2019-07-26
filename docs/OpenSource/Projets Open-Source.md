---
layout: default
title : Projets Open Source
has_children: true
permalink: /projets
nav_order: 99
---

# Quelques projets open source à checker sur Github
Github permet de poster des projets Open Source et disponibles pour tous.
Tous les projets sont libres et peuvent être téléchargés et exécutés.
Les étapes sont simples:

Rendez vous sur **la page Github du projet**

> Clonez ou téléchargez le projet 

![clone or download]({{ site.baseurl }}/assets/images/open/main/download.png)

Ouvrez le pojet dans votre éditeur de choix et tapez la commande suivante dans le dossier du projet. 
```terminal
$ flutter pub get
```
Cette commande sert à installer localement **les packages et plugins** utiliés dans le projet.

Pour lancer le projet dans votre émulateur actif faites :
```terminal
flutter run
```