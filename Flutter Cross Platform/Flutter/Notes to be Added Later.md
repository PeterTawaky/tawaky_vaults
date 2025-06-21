- Anonymous Constructor:
	- use it instead of making instance of the class
	- when want to use class only one time instead of making object
	- one version separated from any other version (constructor)
```dart
MyApp()
Text()
FloatingActionButton()
```
>[!TIP] All widgets in flutter depends on this concept by calling anonymous constructor

- making instance object from the class be like:
	- when want to use this object many times in many places in my code
```dart
FloatingActionButton myButton= FloatingActionButton(/*wanted fields*/);
//now you can use myButton with it's special fields value
```
>[!TIP] most used in creating global keys

set state=> refresh build function