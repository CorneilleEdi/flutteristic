---
layout: default
title: Sweet sheet
description : Utilisation des Bottom Sheets
categories : [fluter, ui, material design]
parent : Tutoriels
---


# Sweet Sheet

![Image principale]({{ site.baseurl }}/assets/images/tuto/sheet_screens/sweet_sheet.jpg)

Avec les smartphones devenant de plus en plus grand, il est difficile de garder une bonne ergonomie dans une application mobile.

Pour plus facilement engager l'interaction de l'utilisateur avec l'application Google a ajouté aux composants du [Material Design ](https://material.io/) le [Bottom sheet](https://material.io/components/sheets-bottom/) ou feuilles de fond.

>Les feuilles de fond sont des surfaces contenant du contenu supplémentaire ancré au bas de l'écran.

Bottom Sheet
{: .image-description}
![bottom sheet from www.material.io]({{ site.baseurl }}/assets/images/tuto/sheet_screens/bottom-sheet.png)

Dans ce tutoriel nous allons créer des Bottom Sheet avec de très beaux designs pour remplacer [les dialogues](https://material.io/components/dialogs/).


Sweet sheet warning
{: .image-description}
![bottom sheet waning]({{ site.baseurl }}/assets/images/tuto/sheet_screens/crop_sweet_sheet.png)

## Création et setup du projet

Faites la commande suivante pour créer un projet Flutter nommé **sweet_sheet**

```terminal
flutter create sweet_sheet
```

puis rendez vous dans le dossier **sweet_sheet**, mettez a jour les packages et lancer votre application avec les commandes suivantes

```terminal
cd sweet_sheet
```

```terminal
flutter pub get
```

```terminal
flutter run
```



Créez les dossiers **pages** et **widgets** ainsi que les fichiers **home_page.dart**,**bottom_sheet.dart** , **large_button.dart** dans le dossier **lib** pour organiser votre code.

```markdown
+-- lib
    +-- pages
    |   +-- home_page.dart
    +-- widgets
    |   +-- bottom_sheet.dart
    |   +-- large_button.dart
    +-- main.dart
```

Maintenant que nous avons notre application en place , nous allons commencer a coder.


Dans **main.dart** , insérer comme proprieté de **ThemeData** l'attribut suivant pour passer au mode sombre (Dark mode).

```dart
brightness: Brightness.dark
```

Votre code dans **main.dart** sera alors

main.dart
{: .file-name}
```dart
void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'Sweet dialog',
      theme: ThemeData(
        fontFamily: 'circular',
        brightness: Brightness.dark,
        primarySwatch: Colors.blue,
      ),
      home: HomePage(title: 'Sweet Sheet'),
    );
  }
}
```


Créons notre bouton qui affichera au clique la feuille de fond.


large_button.dart
{: .file-name}
```dart
class LargeButton extends StatelessWidget {
  final BuildContext context;
  final String text;
  final VoidCallback onclick;

  const LargeButton(
      {Key key, @required this.context, @required this.text, this.onclick})
      : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Container(
      padding: const EdgeInsets.only(bottom: 8.0),
      child: FlatButton(
          padding: EdgeInsets.all(30),
          color: Colors.black45,
          onPressed: onclick,
          child: Container(
            width: double.infinity,
            child: Text(
              '$text',
              textAlign: TextAlign.center,
            ),
          )),
    );
  }
}
```
---

Notre widget **LargeButton** est un **StatelessWidget** qui a comme attribut **le context , le texte et une fonction onClick** qui sera exécutée au clique.

**@required** permet de définir les attribut context et text comme étant des contructeurs optionnels nommés  obligatoires pour le widget **LargeButton**.

---

Passons maintenant  à la création de notre feuille de fond. Pour cela nous allons utiliser une feuille de fond modale .

>Les feuilles de fond modales peuvent être créées et affichées avec la fonction **showModalBottomSheet**.

Voici le contenu de notre fichier **bottom_sheet.dart**


bottom_sheet.dart
{: .file-name}
```dart
class BottomSheets {
  Map<String, List<Color>> sheetColor = {
    'blue': [Color(0xff2979FF), Color(0xff0D47A1)],
    'orange': [Color(0xffFF8C00), Color(0xffF55932)],
    'green': [Color(0xff009688), Color(0xff00695C)],
    'red': [Color(0xffEF5350), Color(0xffD32F2F)],
  };

  showSweetBottomSheet(
      {@required BuildContext context,
      @required String title,
      @required String description,
      @required String type,
      List<FlatButton> actions,
      IconData icon,
      bool haveIcon = false}) {
    showModalBottomSheet<void>(
        context: context,
        builder: (BuildContext context) {
          return Column(
            mainAxisSize: MainAxisSize.min,
            children: <Widget>[
              Container(
                width: double.infinity,
                color: sheetColor[type][0],
                padding: const EdgeInsets.symmetric(
                    horizontal: 24.0, vertical: 24.0),
                child: Column(
                  crossAxisAlignment: CrossAxisAlignment.start,
                  children: <Widget>[
                    Text(
                      title,
                      style: TextStyle(fontSize: 28),
                      textAlign: TextAlign.start,
                    ),
                     _buildContent(haveIcon, description, icon: icon),
                  ],
                ),
              ),
              Container(
                padding: const EdgeInsets.all(8.0),
                color: sheetColor[type][1],
                child: Row(
                    mainAxisAlignment: MainAxisAlignment.end,
                    children: actions),
              ),
            ],
          );
        });
  }
   
    _buildContent(bool haveIcon, String description, {IconData icon}) {
    return Padding(
      padding: const EdgeInsets.symmetric(vertical: 16.0),
      child: SingleChildScrollView(
          child: haveIcon
              ? Row(
                  mainAxisAlignment: MainAxisAlignment.spaceBetween,
                  crossAxisAlignment: CrossAxisAlignment.center,
                  children: <Widget>[
                    Expanded(child: Text(description, style: TextStyle(fontSize: 18), )),
                    Icon(
                      icon,
                      size: 52,
                    )
                  ],
                )
              : Text(description, style: TextStyle(fontSize: 18),)),
    );
  }
}

class BottomSheetType {
  static const SUCCESS = 'green';
  static const DANGER = 'red';
  static const NICE = 'blue';
  static const WARNING = 'orange';
}
```

---


```dart
Map<String, List<Color>> sheetColor = {
    'blue': [Color(0xff2979FF), Color(0xff0D47A1)],
    'orange': [Color(0xffFF8C00), Color(0xffF55932)],
    'green': [Color(0xff009688), Color(0xff00695C)],
    'red': [Color(0xffEF5350), Color(0xffD32F2F)],
  };
```

la portion de code ci-dessus permet de mettre en place un dictionnaire ou une association de chaîne de caractères (String) et de liste de couleur (List< Color >). Nous serons alors en mesure d'utiliser les chaînes de caractères pour récupérer les listes de couleurs.

La méthode **showSweetBottomSheet** permet de designer et d'afficher notre feuille de fond grâce a la fonction **showModalBottomSheet**.

**_buildContent** se sert de son paramètre  **haveIcon** pour déterminer le layout du contenu.
Elle définit si notre feuille de fond contiendra une icône ou pas en utilisant **l'opérateur ternaire ? :**.

```dart
class BottomSheetType {
  static const SUCCESS = 'green';
  static const DANGER = 'red';
  static const NICE = 'blue';
  static const WARNING = 'orange';
}
```

**BottomSheetType** est une simple classe qui expose des constantes. Ces constantes seront plus tard utilisées comme valeur pour spécifier la chaîne de caractère à utiliser pour récupérer la liste de couleurs dans le dictionnaire **sheetColor**.

## Home page

Créons maintenant notre page principale **HomePage** dans le fichier **home_page.dart**.

Nous la créons comme étant un **StatefulWidget** en héritant de la classe **StatefulWidget**.

```dart
class HomePage extends StatefulWidget
```



Déclarons un attribut **title** pour notre classe **HomePage** et passons **title** comme constructeur nommé optionel.

```dart
final String title;

HomePage({this.title});
```

Avant de commencer le layout de la page, créons une instance de la classe **BottomSheets**.

```dart
final MyBottomSheet _myBottomSheet = MyBottomSheet();
```

Passer alors l'attribut **title** comme texte dans le **AppBar** de l'application.

```dart
Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
      ...
)
```

Le composant premier de **HomePage** est une Container avec des margins de 16 a chaque coté.

```dart
Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
      body: Container(
        padding: const EdgeInsets.all(16.0),
      )
      ...
)
```

le Container principal contient ds boutons qui affichent chacun des feuilles de fond différentes en appelant la méthode **showSweetBottomSheet** de notre instance **_myBottomSheet**.

```dart
LargeButton(
              context: context,
              text: 'Simple dialogue',
              onclick: () {
                modal.showSweetBottomSheet(
                  context: context,
                  title: "Lorem Ipsum",
                  description:
                      'Lorem ipsum dolor sit amet, consectetur adipiscing elit. no you condimentum finibus ut ut lorem. Ut pellentesque mauris ut arcu rutrum, at tincidunt arcu tincidunt ',
                  type: BottomSheetType.NICE,
                  actions: [
                    FlatButton(
                      onPressed: () {
                        Navigator.of(context).pop(); // Ferme le bottom sheet
                      },
                      child: Text('CANCEL'),
                    ),
                    FlatButton(
                      onPressed: () {
                        Navigator.of(context).pop(); 
                      },
                      child: Text('CONTINUE'),
                    ),
                  ],
                );
              },
)
```

Le code ci-dessus créer un **LargeButton** avec le texte **Simple dialogue**.

Quand le bouton est cliqué, il affiche une feuille de fond du type **BottomSheetType.NICE** avec un titre, un contenu et deux actions.

```dart
Navigator.of(context).pop()
```

permet de fermer la feuille de fond.

Au final , la classe **HomePage** sera

home_page.dart
{: .file-name}
```dart
class HomePage extends StatefulWidget {
  final String title;

  HomePage({this.title});

  @override
  _HomePageState createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  BottomSheets modal = BottomSheets();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
      body: Container(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          children: <Widget>[
            LargeButton(
              context: context,
              text: 'Simple dialog',
              onclick: () {
                modal.showSweetBottomSheet(
                  context: context,
                  title: "Lorem Ipsum",
                  description:
                      'Lorem ipsum dolor sit amet, consectetur adipiscing elit. no you condimentum finibus ut ut lorem. Ut pellentesque mauris ut arcu rutrum, at tincidunt arcu tincidunt ',
                  type: BottomSheetType.NICE,
                  actions: [
                    FlatButton(
                      onPressed: () {
                        Navigator.of(context).pop(); // To close the dialog
                      },
                      child: Text('CANCEL'),
                    ),
                    FlatButton(
                      onPressed: () {
                        Navigator.of(context).pop(); // To close the dialog
                      },
                      child: Text('CONTINUE'),
                    ),
                  ],
                );
              },
            ),
            LargeButton(
              context: context,
              text: 'Dialog with icon',
              onclick: () {
                modal.showSweetBottomSheet(
                  context: context,
                  title: "Supprimer ce post ?",
                  description:
                  'Cette action supprimera definitivement ce post',
                  type: BottomSheetType.DANGER,
                  haveIcon: true,
                  icon: Icons.delete,
                  actions: [
                    FlatButton(
                      onPressed: () {
                        Navigator.of(context).pop(); // To close the dialog
                      },
                      child: Text('CANCEL'),
                    ),
                    FlatButton(
                      onPressed: () {
                        Navigator.of(context).pop(); // To close the dialog
                      },
                      child: Text('DELETE'),
                    ),
                  ],
                );
              },
            )
          ],
        ),
      ),
    );
  }
}

```


---
Cool, nous avons fini notre application et le résultat est magnifique.

| SUCCESS        | NICE       | DANGER    |
|:-------------|:------------------|:------|
| ![SUCCESS]({{ site.baseurl }}/assets/images/tuto/sheet_screens/success.png)         | ![NICE]({{ site.baseurl }}/assets/images/tuto/sheet_screens/nice.png) | ![DANGER]({{ site.baseurl }}/assets/images/tuto/sheet_screens/danger.png)   |