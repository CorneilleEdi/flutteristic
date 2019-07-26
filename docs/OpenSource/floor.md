---
layout: simple
title: Application de note
parent: Projets Open Source
description : Application de todo list avec sauvegarde dans une base de données SQlite grâce au package Floor (La branche Provider utilise le package Provider pour la gestion des états)
categories : [dart, flutter, open-source]
---

# Application de note avec le package Floor


[Floor task sur Github](https://github.com/CorneilleEdi/floor_task){: .btn .btn-green }


Application de note avec sauvegarde dans une base de données SQlite grâce au package [Floor](https://pub.dev/packages/floor)  (La branche Provider utilise le package Provider pour la gestion des états).
Le packae Floor est une extension du package SQFlite de Flutter.


La bibliothèque Floor fournit un code SQL léger avec une abstraction et un mappage automatique entre les objets en mémoire et les lignes de la base de données, tout en offrant un contrôle total de la base de données à l'aide de SQL.

Il est important de noter que cette bibliothèque n'est pas un ORM complet comme Hibernate et ne le sera jamais. Donc, c'est intentionnel.

### Les fonctionalitées:

- Lister toutes les notes 
- Ajouter une note
- Editer un note
- Supprimer un note
- Supprimer toutes les notes

### Captures d'écrans

| Liste        | Dialogue pour ajouter une note        | Dialogue pour editer une note    |
|:-------------|:------------------|:------|
| ![list]({{ site.baseurl }}/assets/images/open/floor_task/main.png)         | ![list]({{ site.baseurl }}/assets/images/open/floor_task/add.png) | ![list]({{ site.baseurl }}/assets/images/open/floor_task/update.png)   |

task.dart
{: .file-name} 
``` dart 
@entity
class Task {
  @PrimaryKey(autoGenerate: true)
  final int id;

  String title;
  
  final int createdTime;
}
```

Ce code défini le model de la table **Task**  dans la base de données


task_dao.dart
{: .file-name}
``` dart 

@dao
abstract class TaskDao {
  @Query('SELECT * FROM task WHERE id = :id')
  Future<Task> findTaskById(int id);

  @Query('SELECT * FROM task')
  Future<List<Task>> findAllTasks();

  @Query('SELECT * FROM task')
  Stream<List<Task>> findAllTasksAsStream();

  @insert
  Future<void> insertTask(Task task);

  @update
  Future<void> updateTask(Task task);

  @delete
  Future<void> deleteTask(Task task);

  @Query('DELETE FROM task')
  Future<void> deleteAllTask();
}

```


