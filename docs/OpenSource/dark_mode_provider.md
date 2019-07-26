---
layout: simple
title: Theme Changer
parent: Projets Open Source
description : Switcher du mode sombre au mode clair  facilement et en temps réel grâce au package Provider
categories : [dart, flutter, open-source,provider]
---

# Theme Changer (Light mode, Dark mode)

[Flutter dark mode sur Github](https://github.com/CorneilleEdi/flutter_dark_mode){: .btn .btn-green }


Pourquoi ne pas passer au mode Dark?
Cette application illustre la changement de mode. Juste en appuyant sur un boutton vous passerez du mode clair au mode sombre. Rien de plus simple!

Pour la gestion d'état des widgets , le package Provider est utilisé pour garder les chose simples et cohérents.

[Package Provider](https://pub.dev/packages/provider){: .btn .btn-red }



theme.dart
{: .file-name} 
``` dart 
import 'package:flutter/material.dart';
import 'package:shared_preferences/shared_preferences.dart';

class ThemeChanger with ChangeNotifier {
  ThemeData _themeData;

  ThemeChanger(this._themeData);

  getTheme() => _themeData;

  _changeThemePref() async {
    SharedPreferences prefs = await SharedPreferences.getInstance();
    _themeData == ThemeData.light()
        ? prefs.setBool("theme", true)
        : prefs.setBool("theme", false);
  }

  setTheme(ThemeData themeData) {
    _themeData = themeData;
    notifyListeners();

    _changeThemePref();
  }

  getThemePref() async {
    SharedPreferences prefs = await SharedPreferences.getInstance();
    return prefs.getBool("theme");
  }

  String getActualTheme() {
    if (_themeData == ThemeData.light()) {
      return "Light theme mode";
    } else {
      return "Dark theme mode";
    }
  }
}
```

Ce snippet de code permet est la classe model qui controle le changement de theme et qui notifie tous les widgets qui ecoutent les changements
