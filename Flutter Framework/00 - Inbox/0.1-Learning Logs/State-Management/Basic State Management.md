---
tags:
  - state-management
parent: 
type: Permanent Note
deeper: 
against:
---
### Index:
- [[Basic State Management#📌Introduction to State Management]]
- [[Basic State Management#📌setState]]
- [[Basic State Management#📌value-Notifier]]
- [[Basic State Management#📌Change-Notifier]]
- [[Basic State Management#📌Change-Notifier vs Value-Notifier]]
___
### 📌Introduction to State Management
#### What is _State_ in Flutter?
**state** refers to **any data that can change during the lifetime of the app**—like:
- A counter value
- A form input
- User login status
- Whether a button is clicked or not
- Fetched data from an API
#### What is _State Management_?
___
**State management** is the **way you control and update your app's data (state)** and make sure the UI updates when the data changes.
#### Types of State in Flutter:
___
1. **Local State** – managed inside one widget only  
    Example: `setState()` in a `StatefulWidget`
    
2. **Global/App State** – shared across multiple widgets or screens  
#### 🌟 Common State Management Approaches in Flutter:

| Approach         | Description                                | When to Use                          |
| ---------------- | ------------------------------------------ | ------------------------------------ |
| `setState()`     | Built-in, simple state handling            | Small apps or single widget updates  |
| **Provider**     | Official, flexible, and scalable           | Medium to large apps                 |
| **Cubit/Bloc**   | Based on streams and events                | Complex business logic or UI states  |
| **Riverpod**     | More powerful and safe version of Provider | Large apps with deep dependencies    |
| **GetX**         | Lightweight and reactive                   | Quick projects with less boilerplate |
| **MobX / Redux** | Reactive / predictable state patterns      | Special cases or when familiar       |
___
### 📌setState
#### What is setState:
the simplest way of state management. through building the screen again according to the new values of states.

#### Why we need to `setState`:
when you make any change in app logic by changing value of variable the variable changed directly but this change doesn't applied in the screen you just need to tell that you need to build the widgets again cause of change and that's exactly what `setState` do.

#### Mechanism of action:
just go to the nearest build method and build all widgets in it again.

#### Best For:
simple widgets that it's change depends on it self.
ex: Checkbox Widget

#### `setState` Problems:
- when you are trying to update a widget from another widget in different widget tree.
- it build the whole widget in large scale app if any change causing the rebuild of large widgets its' the worst case scenario for your app performance.

#### What we need to do before using it:
you must make any change in logic first. change the value of any variable

>[!NOTE] it must be used only inside stateful widget.

#### Code:
```dart
setState(() {
// write any change code logic
      _counter++; // Update the state, UI will rebuild with the new value of counter
    });
```
___
### 📌value-Notifier
#### What is `ValueNotifier`:
Generic Class contains only one value when this value changes it notifies the listeners and builders

#### Use
- control the state of widget
- fast and easy to use 
- control only one value
- avoid over Engineering in using `ChangeNotifier`
- built-in in the language you don't have to create it

#### Get to the Flow:
1. create the object and set initial value in it:
```dart
  ValueNotifier<int> valueNotifierNumber = ValueNotifier(0); //it can be any type not just int
```
2. access the value inside and change it:
```dart
onTap(){
	valueNotifierNumber.value++;
}
```
3. send this `ValueNotifier` to the widget that will change 
4. now you have to options of use to build or to Listen
	1. Builder Option:
		through using `ValueListenableBuilder` widget and return the rebuild widget
```dart
 ValueListenableBuilder(
      valueListenable: valueNotifierNumber,
      builder: (context, value, child) {
        return Text(
          value.toString(),
          style: TextStyle(fontSize: 30, color: Colors.black),
        );
      },
    );
```
	2. Listener Option:
		by using setState and add Listener exactly as it is used in Change Notifier
```dart
void initState() {
    super.initState();
    widget.controller.addListener(() {
      // listen to the controller
      setState(() {}); // Rebuild the widget when the controller changes
    });
  }
```
___
### 📌Change-Notifier
it's basic to use `setState` in our app but when you keep your code clean and start to use custom widget. you need another solution to change a widget through another widget.

Controller:
بيعمل control لل widget لوحدها مبيغيرش اي حاجة تانية
اقدر اغير في بناء الwidget من خلال الcontroller 

now we will use **`ChangeNotifier`** to make a **custom widget controller**
___
#### Flow of Process:
- create `custom_container_controller.dart` by `ChangeNotifier` class that helps you to send notifications for the widgets how listen to this controller.
- use only one instance in both the trigger widget and the container that's being controlled
- add the listener inside the widget that will be changed
- in the trigger on action access the function inside the controller.
- in changed widget take all values from the controller and listen to the notifications comes from the controller and `setState` each time notified
- don't forget to dispose the controller when you exit the parent screen(the screen you created the controller in) to stop the stream with all listeners to clean memory from all controller data.
#### Creating Controller:
```dart
class CustomContainerController extends ChangeNotifier {
  // Attributes that can be controlled
  double width = 200.0; //initial values
  double height = 200.0;
  Color color = Colors.blue;

  void changeContainerAttributes() {  //uses the attributes inside the controller
    width = Random().nextDouble() * 300.0; // Random width between 0 and 300
    height = Random().nextDouble() * 300.0; // Random height between 0 and 300
    color = Color.fromARGB(
      255,
      Random().nextInt(255), // Random color from 0 to 255
      Random().nextInt(255),
      Random().nextInt(255),
    ); // Random color
    notifyListeners(); //send notification to listeners
  }
}
```
___
#### Inside the Controlled(Listener) Widget:
- receives an instance of controller to access attributes from it
- the place to `setState`
- uses the attributes that comes from the controller.
- must listen here to the notifications
```dart
void initState() {
    super.initState();
    widget.controller.addListener(() {
      // listen to the controller
      setState(() {}); // Rebuild the widget when the controller changes
    });
  }
```
___

#### Parent Widget
- the place you crate the instance of controller 
- the place to dispose the controller.
- place to trigger the function inside the  controller through the same instance created.
```dart
 void dispose() {
    customContainerController.dispose();
    super.dispose();
  }
```
```dart
 onPressed: () {
	customContainerController.changeContainerAttributes(); //trigger
  },
```
___
### 📌Change-Notifier vs Value-Notifier
#### ⚖️ Summary Table

|Feature|`ChangeNotifier`|`ValueNotifier<T>`|
|---|---|---|
|Stores multiple values?|✅ Yes|❌ No (only one `value`)|
|Notifies manually?|✅ Yes (`notifyListeners()`)|❌ No (automatic on `.value` change)|
|Lightweight?|❌ No (more boilerplate)|✅ Yes|
|Use with Provider?|✅ Yes|✅ Yes|
|Best use case|App-wide or complex state|Simple single value updates|
