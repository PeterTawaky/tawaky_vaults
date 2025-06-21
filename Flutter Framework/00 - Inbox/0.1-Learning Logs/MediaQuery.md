---
tags:
  - responsive-adaptive
parent: "[[Responsive]]"
type: Permanent Note
deeper: 
against:
---
> Widget used for making Responsive UI design
- get current orientation ( landscape / portrait )
- get current height
- get current width
```dart
double width = MediaQuery.of(context).size.width;
double height = MediaQuery.of(context).size.height;
Orientation orientation = MediaQuery.of(context).orientation;

debugPrint(width.toString());
debugPrint(height.toString());
debugPrint(orientation.toString());
```
> you can multiply the width and height with the fraction you want to take a size according to the screen size
- Ex:
```dart
height * 0.5
width * 0.2
```
> you can use orientation for changing the sizes according to the mobile rotate state
- Ex:
```dart
 height: orientation == Orientation.landscape
	? height * 0.2
	: height * 0.3,
```


