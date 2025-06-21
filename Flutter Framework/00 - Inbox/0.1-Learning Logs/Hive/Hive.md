---
tags:
  - local-data-base
parent: "[[Local Data]]"
type: Permanent Note
deeper: "[[Hive.excalidraw]]"
against: "[[sqflite]]"
---
Index:
[[Hive#📌Intro]]
[[Hive#📌Code with Hive in details]]

___
### 📌Intro:
#### Hive Behavior:
> NoSQL Database Stores data in App Cache
> Stores the Data in `Boxes` in the form of Map< Key , value >
> each box has reference

#### Needed Packages:
[hive package - All Versions](https://pub.dev/packages/hive/versions)
[hive_flutter package - All Versions](https://pub.dev/packages/hive_flutter/versions)
#### Hive is the Fastest one:
as it access data through RAM not ROM
![[Hive-fastest]]
>[!NOTE] >Key in Hive can be int or String

>[!NOTE] >Value can be anything even array or an object from class

>[!TIP] > in hive the integer keys is arranged in a list that each key has it's own index, so when you try to add or get data through index the string keys is out of this context 

___
### 📌Code with Hive in details:
#### Initialize Hive and create my box with id:
```dart
void main() async {
  WidgetsFlutterBinding.ensureInitialized(); //ensure initialization
  await Hive.initFlutter(); //initialize hive
  await Hive.openBox('notes'); //create a box with id if exist open if not create one
  runApp(NotesApp());
}
```

#### Use Box with Specific Values:
```dart
await Hive.openBox<String>("names");
```
#### Create a variable to carry the Box you created:
```dart
Box box = Hive.box('notes'); //take my box in variable to use
```
#### Create an empty List to carry all values in database:
```dart
List<Map<String, dynamic>> notesData = []; //a list to carry the data in my data base
```
___
### 📌Operations:
#### 📃Put data in Hive:
	if key found put value if not, create it then put value
##### put:
	one value only
```dart
box.put(key,value)
```
##### put-All:
	a full map of many keys and values
```dart
box.put({
	key:value
	key:value
	key:value
})
```
##### put-at:
	deals only with integer keys which is arranged in a list
	if you put index out of range exist it will through an error
```dart
box.putAt(index,value)
```
#### 📃Add data in Hive:
	deals only with integer keys so you don't have to create key it's created automatically
	take the place after the largest integer key found
##### add:
```dart
box.add(value)  //now the key of this value is 0
```
##### add-All:
	list of values
```dart
box.addAll([
value,  // key:0
value,  // key:1
value,  // key:2
value,  // key:3
])
```
#### 📃Get data in Hive:
	if there is no value for this key then it will get null
##### get:
```dart
box.get(key)
```
- What if you want to get untraditional value instead of null(when there is no value):
```dart
box.get(key,defaultValue:true)  //if found value return it if not return true
```
##### get-At:
	deals with index
```dart
box.getAt(index)
```
##### get all box values:
```dart
box.values
```
#### 📃Delete data in Hive:
##### delete:
```dart
box.delete(key);
```
##### delete-All:
```dart
box.deleteAll([
	key,
	key,
	key
]);
```
##### delete-At:
```dart
await box.deleteAt(index);
```
##### clear:
	delete all data in the box, the box is still exist but totally empty.
```
box.clear();
```
##### delete-from-disk:
	delete the box itself from the local storage with all keys and values inside it.
```dart
await box.deleteFromDisk();
```
___
#### 📃Add data in the box in the form of map:
```dart
void addNote({required String title, required String description}) async {
    await notesRef.add(
      {
        //adding a map to the box
        'title': title,
        'description': description,
      },
    );
    getNotes();   //to add the new data to the list and set state
  }
```

>[!Note] each note map is added automatically create a key to reach it
___
### Get Data through Keys
```dart
void getNotes() {
    //make loop to save data in my list
    setState(() {
      notesData = notesRef.keys.map((key) {
        final currentNote = notesRef
            .get(key); //current node is a map which i can access it's elements
        return {
          'key': key,
          'title': currentNote['title'],
          'description': currentNote['description'],
        };
      }).toList();
    });
    debugPrint(notesData.length.toString());
  }
```
___
### Delete data through Key:
```dart
void deleteNote({required int key}) {
    notesRef.delete(key);
    getNotes();
  }
```
___
### Edit data through Key:
```dart
updateNote() {
    notesRef.put(noteKey, {
      'title': titleController.text,
      'description': descriptionController.text,
    });
  }
```
___
## Search for Data:
```dart
filterData({required String input}) {
    setState(() {
      filteredList = notesData  //a list you create to carry filtered data
          .where((element) => element['title']
              .toString()
              .toLowerCase()
              .startsWith(input.toLowerCase()))
          .toList();
    });
  }
```
___
### 📌Hive Fastest Use in Real Projects:
#### 1.Download the Packages:
##### in the Dependencies
- Hive
- Hive Flutter
##### in the dev Dependencies
- Hive Generator
- Build Runner
#### 2.Create the Entity Adapter
1. before the whole screen use: `part 'book_entity.g.dart';` => will be generated
2. before the entity write: `@HiveType(typeId: 0)`
3. before each field in this entity write `@HiveField(0)
4. then run the command in the terminal
```
flutter packages pub run build_runner build
```
##### Ex:
```dart
import 'package:hive/hive.dart';

part 'book_entity.g.dart';
@HiveType(typeId: 0)
class BookEntity {
  @HiveField(0)
  final String bookId;
  @HiveField(1)
  final String? image;
  @HiveField(2)
  final String title;
  @HiveField(3)
  final String? author;
  @HiveField(4)
  final num? price;
  @HiveField(5)
  final num? rating;
  
  BookEntity({
    required this.bookId,
    required this.title,
    this.author,
    this.image,
    this.price,
    this.rating,
  });
}
```
#### 3.Register the Adapter you have Created and Open the Hive Box:
```dart
void main() async {
  await Hive.initFlutter();
  Hive.registerAdapter(BookEntityAdapter());
  await Hive.openBox(CacheKey.books);
  runApp(BooklyApp());
}
```