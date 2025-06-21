---
tags:
  - fire-base
  - BaaS
parent: "[[Intro to Firebase]]"
type: Permanent Note
deeper: 
against:
---
## Activate `Cloud Firestore` via Firebase Project:
- create __`FireStore`__ database: [Firebase console](https://console.firebase.google.com/project/mastering-fire/overview)
## Activate Authentication via my Flutter Project: [Cloud Firestore](https://firebase.flutter.dev/docs/firestore/usage)
1. upload package: [cloud_firestore](https://pub.dev/packages/cloud_firestore) and [firebase_database](https://pub.dev/packages/firebase_database/install)
2. import the package: 
```dart
import 'package:cloud_firestore/cloud_firestore.dart';
```
3. now start collection that will carry the documents in it:
```dart
CollectionReference collection = FirebaseFirestore.instance.collection('collection');
```
___
### 1.Insert Data in Specific Document:
> Data is Inserted in the form of Map<String, dynamic>

```dart
Future<void> addCategory() {
    // Call the user's CollectionReference to add a new user
    return collection
        .add({'name': categoryController.text})
        .then((value) => debugPrint("cat"))
        .catchError(
            (error) => debugPrint("Failed to addegory is added user: $error"));
  }
```
>[!Note] > don't forget to make sure that data you take is not empty

___
### 2.Get Data:
#### 2.1Get a Specific Collection:
- function of getting data from firebase:
```dart
  List<QueryDocumentSnapshot> data = []; //list of empty data
getCollectionData() async {
    QuerySnapshot response =
        await FirebaseFirestore.instance.collection('categories').get();
    data.addAll(response.docs); //fill the data in the list you have created
    print(data);
    setState(() {});  //to appear the changes in UI
  }
```
- call this function in the `initState`:
```dart
void initState() {
    getCollectionData();
    super.initState();
  }
```
- access this data in any list builder widget(`ListView.builder` - `GridView.builder`):
```dart
Text('${data[Index]['name']}')
```
___
### 3.Removing Document Data:
> we can remove the document and all it's items by knowing the `Document ID`
> after delete the item you should navigate to the same screen you are in to show the changes

>[!Note] > use any widget to ensure if the user want really to delete the data or it's only pressed by mistake.

```dart
 AwesomeDialog(
	context: context,
	animType: AnimType.scale,
	dialogType: DialogType.warning,
	body: Center(
	  child: Text(
		S.of(context).deleteMsg,
		style: Theme.of(context)
			.textTheme
			.bodyMedium!
			.copyWith(color: AppColors.kBlack),
	  ),
	),
	btnOkOnPress: () async {
	  await FirebaseFirestore.instance
		  .collection('categories')
		  .doc(data[Index].id)  //reach to the document id
		  .delete();
	  context.pushReplacementNamed(AppRoutes.homeScreen);
	},
	btnCancelOnPress: () {})
	.show();
},
```
___
## 4.Different User Different Data:
> make each user has his own data and display different data for each one.
> this can happen by using `Unique ID` for Each User
### How to access the user Unique id:
```dart
FirebaseAuth.instance.currentUser!.uid
```
### While Inserting Data:
```dart
Future<void> addCategory() {
    return categories
        .add({
          'name': categoryController.text,
          'id': FirebaseAuth.instance.currentUser!
              .uid,                                                               //each user has different id to bring different data
        })
        .then((value) => debugPrint("cat"))
        .catchError(
            (error) => debugPrint("Failed to addegory is added user: $error"));
  }
```
### While Display Data:
```dart
getCollectionData() async {
    QuerySnapshot response = await FirebaseFirestore.instance
        .collection('categories')
        .where('id', isEqualTo: FirebaseAuth.instance.currentUser!.uid)  //get only data in the user id
        .get();
    data.addAll(response.docs); //fill the data
    print(data);
    setState(() {
      isLoading = false;
    });
  }
```
>[!Summary] >Different user Different Data

___
### 5.Update Data:
> need the id of the document that will be edited
> need the current data will be edited
```dart
Future<void> editCategory() {
    return categories
        .doc(widget.documentationData.documentationId) //must take the id from the constructor
        .update({'name': categoryController.text}) //the new text to update from the text field
        .then((value) => debugPrint("data Updated"))
        .catchError((error) => debugPrint("Failed to update the data: $error"));
  }
```
>make the previous data appears in the text form field:
```dart
    categoryController.text = widget.documentationData.oldData;  //data taken from the constructor
```
___
### 5.Set Data:
>  if document ID found Update it if not  then Create it
```dart
 Future<void> setCategory() {
    return categories
        .doc('123456789') //must take the id
        .set({
          'name': categoryController.text,
        }) //the new text to update
        .then((value) => debugPrint("data Updated"))
        .catchError((error) => debugPrint("Failed to update the data: $error"));
  }
```
>[!Note] > in the previous code the id is not set so the value of it will be deleted

> so we can use `setOption`to save the last data not updated
```dart
 Future<void> setCategory() {
    return categories
        .doc('123456789') //must take the id
        .set({
          'name': categoryController.text,
        },
        SetOptions(merge: true),      //the different that id will not removed
        ) //the new text to update
        .then((value) => debugPrint("data Updated"))
        .catchError((error) => debugPrint("Failed to update the data: $error"));
  }
```
___
please anser simply what is the difference between :

QuerySnapshot .docs

DocumentSnapshot .exist map

- **QuerySnapshot**: A collection (list) of documents. You get this when you run a query that matches **multiple documents**.
    
- **DocumentSnapshot**: A **single document**. You get this when you fetch **one specific document** by its path. it's totally like a map. but how to read it as a map
___
- If you do `FirebaseFirestore.instance.collection('users').get()`, you get a **QuerySnapshot** (all users).
    
- If you do `FirebaseFirestore.instance.doc('users/user1').get()`, you get a **DocumentSnapshot** (only user1).
___
```dart
QuerySnapshot snapshot = await FirebaseFirestore.instance.collection('users').get();

for (var doc in snapshot.docs) {
  print(doc.id);
  print(doc['name']);
}
```
```dart
DocumentSnapshot doc = await FirebaseFirestore.instance.collection('users').doc('user1').get();

if (doc.exists) {
  print(doc.id);
  print(doc['name']);
} else {
  print('No such document');
}
```