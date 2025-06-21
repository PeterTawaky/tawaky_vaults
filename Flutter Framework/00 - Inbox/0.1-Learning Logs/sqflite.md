---
tags:
  - local-data-base
parent: "[[Intro to Database With Flutter]]"
type: Permanent Note
deeper: 
against: "[[Hive]]"
---
## 1. download the package: [`sqflite`]([sqflite | Flutter package](https://pub.dev/packages/sqflite))
## 2. Steps
1. Create database (one time)
2. create tables (one time)
3. open database (each time)
4. go on operations
## 3. operations on this Database:
1. insert data
2. get from database
3. update in database
4. delete from database
5. remove database
## 4. main methods in Database Class:
```dart
 import 'package:path/path.dart';
 //initialize for sqflite
  initalDb() async {
    //path in your device
    String path = await getDatabasesPath(); //function to determine path
    String databaseName = 'tawaky.db'; //name of data base with it's extension
    String databasePath = join(path, databaseName); //   path/name.db
    //opening your data base
    Database myDb = await openDatabase(
      version: 1, //change it when you want to add new column after database created that will trigger the _onUpgrade method
      onUpgrade: _onUpgrade,  //execute only when the version changes
      databasePath,
      onCreate: _onCreate, //to build tables excecute only one time when creating the database
    );
    return myDb;
  }
```
## _onUpgrade function
```dart
_onUpgrade(Database db, int oldVersion, int newVersion) async {
    print("new version updated");
    await db.execute("ALTER TABLE notes ADD COLUMN color TEXT"); //when version changes a new column will be added
  }
```

> [!IMPORTANT] > when you want only to create one table in this database
```dart
_onCreate(Database db, int version) async {
    //يتم استدعائها مرة واحدة فقط عند إنشاء الداتابيز
    //creating tables
    //notes is the table name wich has columns(id,note)
    await db.execute('''
    CREATE TABLE "notes"(  
      "id" INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,
      "title" TEXT NOT NULL,
      "note" TEXT NOT NULL
    )
    ''');
    print('create "notes" table in your Database');
  }
```

> [!IMPORTANT] > when you want to create many tables in this database use ==Batch==

```dart
_onCreate(Database db, int version) async {
    Batch batch = db.batch();
	//first table
    batch.execute('''
    CREATE TABLE "notes"(  
      "id" INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,
      "title" TEXT NOT NULL,
      "note" TEXT NOT NULL
    )
    ''');
    //second table
    batch.execute('''
    CREATE TABLE "students"(  
      "id" INTEGER NOT NULL PRIMARY KEY AUTOINCREMENT,
      "title" TEXT NOT NULL,
      "note" TEXT NOT NULL
    )
    ''');
   await batch.commit();  //excecute all operations in one time
    print('create "notes" table in your Database');
    print('create "students" table in your Database');
  }
```

### How Deleting the Database Affects It:

- **Deleting the database** means that the underlying SQLite file is removed from the device. This causes any subsequent attempts to access the database to fail because the connection to the deleted database is no longer valid.
- When you try to perform operations (like querying or inserting data) after deleting the database, the database connection is considered closed, leading to the error you're seeing: `database_closed 2`.