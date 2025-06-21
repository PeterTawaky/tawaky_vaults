---
tags:
  - state-management
parent: "[[Intro to State Management]]"
type: Permanent Note
deeper: "[[Provider as an Inherited Widget]]"
against: 
---
### Index:
- [[Provider#📌Provider as a State Management]]
- [[Provider#📌Provider as an Inherited Widget]]
___
- First install package: [provider](https://pub.dev/packages/provider)
### 📌Provider as a State Management:
#### 1. Create Provider Class:
- states (variables-that will change during the app)
- getter
- methods
- `notifyListeners()` inside the method
```dart
import 'package:flutter/material.dart';
class CounterProvider with ChangeNotifier {
  //put your states here
  int _counter = 0;
  int get counter => _counter;
  void increment() {
    _counter++;
    notifyListeners();  //send notification to all listeners 
  }
}
```
#### 2. Provide an instance of your Provider:
- before use the provider states or methods in your widget you should wrap the widget that will be changed with: `ChangeNotifierProvider`
```dart
ChangeNotifierProvider(
	create: (_) => CounterProvider(), //class provider created
	child: MyWidget(),
	)
```
- or Deal with more than one Provider through: `MultiProvider`
```dart
MultiProvider(
  providers: [
	ChangeNotifierProvider(create: (_) => CounterProvider()),
	ChangeNotifierProvider(create: (_) => CartProvider()),
  ],
  child: const MyApp(),
),
```
#### 3. Use the Provider:
##### 3.1 Get a state(variable) from your Provider:
```dart
Text(context.watch<CounterProvider>().counter.toString())
```
##### 3.2 Trigger a Method in Provider:
```dart
context.read<CounterProvider>().increment();
```
>[!TIP] > in this Level the Provider rebuild the whole screen when trigger the method. the next level I need to rebuild only the needed widget that will change. for best App Performance.

___
#### Enhancing Code:
- rebuild only the changed widget.
##### Consumer Widget:
	wrapped to the widget that will changed and it will be the only widget will be rebuilt.
```dart
Consumer<CounterProvider>(
  builder: (context, ref, child) {
	return Text(
	  context.watch<CounterProvider>().counter.toString(),
	);
  },
),
```
##### Selector Widget:
	used when you hava a provider that contains many states(variables) in it and you want only to rebuild the widget when changing only a specific variable in the provider not all variables change cause rebuild
```dart
Selector<CounterProvider, int>(
  builder: (context, ref, child) {
	log('Widget rebuilded');
	//widget that will be rebuild
	return Text(context.watch<CounterProvider>().cart.toString());
  },
  selector: (context, value) => value.counter,//the only variable that will cause widget rebuild
),
```
![[Excalidraw-provider state management]]
___
### 📌Provider as an Inherited Widget:
- provider is not recommended to use as a state management.
- but it's best practice to use it as Inherited widget as it wrapped with Inherited widget
you can pass any value any where
![[Excalidraw-Provider as Inherited Widget]]
```dart
FormInput formInput=FormInput()

Provider.value(
	value: formInput,
	child: Parent Widget(
		//now any widget in this tree can access this value
	)
)
//or---------------------------------------------------------
rovider(
	create:(context)=>FormField(),  //instance is created here
	child: Parent Widget(
		//now any widget in this tree can access this value without any need to pass data from widget to another
	)
)
```
### How to Access:
```dart
context.read<FormInput>().tffOne // a value in the FormInput
```