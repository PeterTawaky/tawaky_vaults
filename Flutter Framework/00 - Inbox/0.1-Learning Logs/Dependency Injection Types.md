---
tags:
  - design-principles
parent: "[[Dependency Injection]]"
type: Permanent Note
deeper: 
against:
---
1. Constructor Injection:
	- set the class through constructor
```dart
class Car {
  final Engine engine;
  Car(this.engine);
}
```
problem of this scenario is each time you create an instance of car you should create an instance of engine
2. **Setter Injection**
	- set the the class through setter function.
```dart
class Car {
  Engine? engine;
  void setEngine(Engine engine) { //will only used one time
    this.engine = engine;
  }
}
```
in this way you will only create one instance of engine even if you created many instances of cars.
3. Service Locator
	- a big container containing all the dependencies and can inject it any time you want to any class.
	- this is the way we will use in our flutter application