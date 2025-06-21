---
tags:
  - local-data-base
parent: "[[Intro to Database With Flutter]]"
type: Permanent Note
deeper: "[[cache_helper]]"
against:
---
>  Local File System that Stores Simple Data in my App Cache
> Stores the Data in the form of Map< Key , value >
## A Ready File For Use: [[cache_helper]]
___
### Some real uses:
- save app theme
- save app language
- save state of login or logout
- save profile picture path
### Download Package: [shared_preferences](https://pub.dev/packages/shared_preferences)
### Create an object of shared preference to use it:
- declaration
- assignment

2. import the package:
```
import 'package:shared_preferences_android/shared_preferences_android.dart';
```
3. create a variable that will be an object from the shared Preference:
```dart
static late SharedPreferences sharedPreferences;
```
4. now Initialize this variable to be an object:
```dart
static cacheInitialization() async {
    sharedPreferences = await SharedPreferences.getInstance(); //method to return object
  }
```
### Make a class to handle all operations:
- set =>requires( key , value )
- get => requires (key)
- delete => requires (key)

#### Set Data:
```dart
//set any type of data
  static Future<bool> setData({required String key, required dynamic value}) async {
    if (value is int) {
      await sharedPreferences.setInt(key, value);
      return true;
    } else if (value is double) {
      await sharedPreferences.setDouble(key, value);
      return true;
    } else if (value is bool) {
      await sharedPreferences.setBool(key, value);
      return true;
    } else if (value is String) {
      await sharedPreferences.setString(key, value);
      return true;
    } else {
      //only if the data is not saved
      return false;
    }
  }
```
___
#### Set Data:
```dart
//get any type of Data
  static dynamic getData({required String key}) {
    return sharedPreferences.get(key);  //can get any type of data
  }
```
#### Delete Item:
```dart
//delete item
  static void deleteItem({required String key}) {
    sharedPreferences.remove(key);
  }
```

#### Clear Cache:
```dart
//clear cache
  static void clearData() {
    sharedPreferences.clear();
  }
```
___
## We Have to make sure about Initialization before the app run:
```dart
Future<void> main() async {
 //never build the app until the initialization is done
WidgetsFlutterBinding.ensureInitialized(); 
await CachedData.cacheInitialization();
runApp(SmartHome());
}
```
