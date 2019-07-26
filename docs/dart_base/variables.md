---
layout: default
title: 01 - Les variables
description : Définition des variables et des constantes en Dart
parent : Dart - les bases
categories : [dart, dart-base]
nav_order : 1
---


## Table des matières
{: .no_toc .text-delta }

1. TOC
{:toc}


# Les règles bases de Dart

- Un code Dart s'exécute toujours en commençant par la fonction **main(  ){   }**. Alors il est important de placer votre code à exécuter dans cette fonction.
- Une ligne complète en Dart se termine toujours par un point virgule  **;**
- Il est possible d'écrire des commentaires en Dart. Les commentaires sont des lignes qui ne n'executent pas. Pour faire un commentaire , il suffit de mettre deux **slash //** au début de la ligne. Pour un commentaire multiligne, le plus simple est d'ecrire le commentaire entre **/\*** et ***/**

# Test 

Avant de commencer nous allons écrire un petit programme et exécuter pour s'assurer que tout marche parfaitement. Dans le tutoriel précédent nous avons installé le SDK Dart , l'éditeur de texte et nous avions fait les configurations qui s'imposent. Maintenant nous allons tester tout cela.

Les fichiers contenant du code écrit en Dart ont toujours l'extension **.dart**

Dans votre éditeur de texte, copiez et collez le code suivant dans un fichier **main.dart**. (Vous pouvez nommer ce fichier autrement)

main.dart
{: .file-name}
```dart
void main(){
    print("Hey, tout marche");
}
```

Ensuite ouvrez votre terminal intégré en faisant **Ctrl+`** ou ouvrez simplement un terminal (Invite de commande sur Windows), rendez vous dans le dossier contenant votre fichier dart et faites la commande suivante:

```terminal
dart main.dart
```

>  N'oubliez pas de changer **main** par le nom de votre fichier dart.

Pour exécution avec IntelliJ IDEA ou Android Studio , exécutez votre programme en cliquant sur **Run**. 

![Android studio run](https://flutter.dev/assets/tools/android-studio/main-toolbar-857fe8c36d38020e27b502ec643ea8b1716edbe150cc6e39e3560f8fb7bda5b2.png)

Si tout fonctionne bien, vous devriez avoir le résultat suivant:

 ```terminal
$ dart main.dart

  Hey, tout marche
 ```

Si vous avez ce message alors félicitation. Votre code a été exécuté avec succès 👍.



# Les variables


Les variables permettent d'associer une valeur ou une chose à un nom. Dans le langage informatique, c'est une référence à une adresse mémoire. Ce nom permettra plus tard d'accéder à cette valeur et même de la modifier.

Le nom d'une variable obéit à des impératifs ou règles changeant selon les langages. Toutefois, une règle absolue est qu’un nom de variable peut comporter des lettres et des chiffres, mais qu’il exclut la plupart des signes de ponctuation, en particulier les espaces. Une variable peut aussi commencer par ou comporter des underscores **_** . Mais une variable qui commence par un underscore a une signification particulière que nous serons amenés à voir plus tard.


## Déclaration d'une variable

La syntaxe pour déclarer une variable dans le langage Dart est très simple.

```dart
var nom_de_la_variable = la_valeur;
```

le mot clé **var** permet de signifier que nous sommes entrain de déclarer une variable.

Example

```dart
var nom = 'Jean Luc';
var age = 16;
var isPremium = true;
var langages = ['Python', 'Javascript', 'Java', 'Kotlin'];
```

Il est strictement interdit de déclarer des variables ayant le même nom. C'est une erreur qui empèchera votre programme d' ètre exectué.
{: .tip .tip-danger}

## Les constantes

Les constantes sont des variables qui, après leur déclaration ne peuvent pas être modifiées.

> les constantes peuvent être utilisées pour stocker des valeurs comme des adresses URL, des chemins vers un fichier, des ID d'utilisateur.

### Déclaration d'une constante
Pour déclarer une constante, on utilise le mot clé **const** ou **final**. On utilise **const** pour déclarer des constantes à la compilation mais dans l'ensemble ces deux mots clés permettent de faire la même chose (déclarer une constante).

```dart
var nom_de_la_constante = la_valeur;
```

Exemple :

```dart
const url = 'www.flutteristic.dev';
final userId = "If4hgt8374Nftdgo094";
var langues = ['francais', 'Anglais', 'Espagnol'];
```



Si vous essayez de changer une constante dans votre programme, cela causera une erreur.
{:.tip .tip-danger }

```
// Error: a final variable can only be set once.
// Une constante ne peut être déclarée qu'une seule fois
```

# Pratique

variable.dart
{: .file-name}
```dart
void main(){
    const nom = "Steve Jobs"
    var age = 50
    
    //Affichage du nom et de l'age
    print(nom);
    print(age)
}
```

la fonction **Print** permet d'afficher le message qui lui est passé en paramètre dans la console.
{:.tip .tip-warning }

output
{: .file-name}
```
Steve Jobs
50
```