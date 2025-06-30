---
tags: 
status: 
parent: 
type: Permanent Note
deeper: 
against:
---
### Index:
- [[Responsive & Adaptive UI#📌Definition]]
- [[Responsive & Adaptive UI#📌Achieving Adaptive]]
- [[Responsive & Adaptive UI#📌Widgets to Achieve Responsive]]
- [[Responsive & Adaptive UI#📌Achieving Responsive through Package]]
- [[Responsive & Adaptive UI#📌Reference]]
___ 
### 📌Definition:
#### Responsive:
	solve the problem of UI
- making the UI available with not fixed sizes but depends on logical sizes according to the screen size
#### Adaptive:
	solve the problem of UX
- build different UI for Different Devices when the size of Device is totally different:
	- mobile 
	- tablet
	- desktop
___
### 📌Achieving Adaptive:
	this can happen through the widget LayoutBuilder
- Widget used for making Adaptive UI design
- it provides context-based screen constrains for widget building
- build different UI according to the screen width through the __constraints__
#### 📃Do It In Code:
- inside the Scaffold `AppBar`:
	- only view in tablet and mobile
```dart
appBar:
  !context.isDesktop
	  ? AppBar(
		backgroundColor: Color(0XFFDBDBDB),
		leading: IconButton(
		  icon: Icon(Icons.menu, color: Colors.black),
		  onPressed: () {
			scaffoldKey.currentState!.openDrawer();
		  },
		),
	  )
	  : null,
```
- inside the Scaffold body:
```dart
LayoutBuilder(
      builder: (context, constraints) {
        if (constraints.maxWidth > 1000) {
          //for windows
          return DesktopLayout();
        } else if (constraints.maxWidth > 600) {
          //for tablet
          return TabletLayout();
        } else {
          //for mobile
          return MobileLayout();
        }
      },
    );
```
___
### 📌Widgets to Achieve Responsive:
- `MediaQuery`
#### Media Query:
- get Current height and width of the screen
- get current orientation ( landscape / portrait )
##### 📃Apply on Code:
```dart
final size = MediaQuery.sizeOf(context);
final orientation = MediaQuery.orientationOf(context);
final textScaleFactor = MediaQuery.textScaleFactorOf(context);
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
##### Apply best Practice:
- use `blocWidth` and `blocHeight`
```dart
import 'package:flutter/material.dart';
extension SizeExtension on BuildContext {
  Size get screenSize => MediaQuery.sizeOf(this);
  
  double get screenWidth => screenSize.width;
  double get screenHeight => screenSize.height;
  
  double get blockWidth => screenWidth / 100; //1% of screen width
  double get blockHeight => screenHeight / 100; //1% of screen height
  
  bool get isMobile => screenWidth < 600;
  bool get isTablet => screenWidth >= 600 && screenWidth < 1024;
  bool get isDesktop => screenWidth >= 1024;
}
```
- access it:
```dart
context.blockWidth  * n
context.blockHeight * n
```
___
### 📌Achieving Responsive through Package:
	use the package: flutter_screenutil
- Scaling UI elements for different screen sizes:
	- flexible font      `.sp`
	- flexible width     `.w`
	- flexible height    `.h`
	- flexible radius    `.r`
#### 📃Apply it on Code:
- make it parent to the `MaterialApp` widget:
```dart
@override
Widget build(BuildContext context) {
 final logicalWidth =
        WidgetsBinding
            .instance
            .platformDispatcher
            .views
            .first
            .physicalSize
            .width /
        WidgetsBinding.instance.platformDispatcher.views.first.devicePixelRatio;
	return ScreenUtilInit(
		designSize: HelperFunctions.getDesignSize(logicalWidth),
		minTextAdapt: true, 
		splitScreenMode: true,
		builder: (_ , child) {
			return MaterialApp( 
				debugShowCheckedModeBanner: false,
				title: 'First Method', 
				theme: ThemeData( 
					primarySwatch: Colors.blue,
					textTheme: Typography.englishLike2018.apply(fontSizeFactor: 1.sp),
				),
				home: child,
			); 
		},
		child: const HomePage(title: 'First Method'),
	); 
}
```
___
### 📌Tips & Notes:
>[!TIP] >  for Spaces Between Items use `MediaQuery` scale, for items sizes use: screen-util scale


___
### 📌Reference:
[Responsive & Adaptive design | Flutter](https://docs.flutter.dev/ui/adaptive-responsive)
