---
tags:
  - responsive-adaptive
parent: "[[Responsive]]"
type: Permanent Note
deeper: 
against:
---
>Scaling UI elements for different screen sizes

> we can do all responsive needs using package: [flutter_screenutil](https://pub.dev/packages/flutter_screenutil)
- flexible font       (.sp)
- flexible width     (.w)
- flexible height    (.h)
- flexible radius    (.r)
### Add this as a Parent Widget to the App:
```dart
@override
Widget build(BuildContext context) {
	return ScreenUtilInit(
		designSize: const Size(360, 690),  //the size of screen that designer work on it on figma
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

### Font Size According to Screen Size:
```dart
fontSize: 18.sp
```
### Width & Height According to Screen Size:
```dart
height: 250.h, 
width: 250.w, 
```
### Radius and Curves According to Screen Size:
```dart
borderRadius: BorderRadius.Circular(18.r)
```