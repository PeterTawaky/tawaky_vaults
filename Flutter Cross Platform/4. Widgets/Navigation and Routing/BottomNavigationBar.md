
## Fields:
- items: [ `[[BottomNavigationBarItem]]` ]
- `currentIndex`:  `_currenIndex`   // a variable it's default value is zero
- `backgroundColor`:
- elevation:
- `selectedIconColor`:
- `unselectedIconColor`:
- `selectedFontSize`:
- `selectedLabelStyle`: 
- `onTap` : (`newIndex`){ `_currenIndex`= `newIndex`}  //to change the navigation don't forget to change the state
___
## How to Change the Screen according to the current Index?
- create a List of Widgets:
```dart
List<Widget>Screens[
	ScreenOne(),
	ScreenTwo(),
	ScreenThree(),
];
```
- apply this change in the body
```dart
body:Screens.elementAt[_currentIndex]  //change the index according two Bottom Nav Bar
```