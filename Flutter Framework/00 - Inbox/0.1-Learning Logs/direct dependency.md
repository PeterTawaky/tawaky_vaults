---
tags:
  - design-principles
parent: "[[Dependency]]"
type: Permanent Note
deeper: 
against: 
aliases:
  - Tight Coupling
---
### Problem Case Study:
lets have to classes connected with each other like Dependency Class engine and some other classes Like:
- car 
- motorcycle
- airplane
- etc..
the thing that is common between all of them is that they all need engine.
```dart
class Engine {
  void start() {
    print("Engine started");
  }
}

class Car {
  Engine engine = Engine(); // this line is the problem
  void start() {
    engine.start();
    print("Car started");
  }
}
class Airplane {
  Engine engine = Engine(); // this line is the problem
  void start() {
    engine.start();
    print("Airplane started");
  }
}
class MotorCycle {
  Engine engine = Engine(); // this line is the problem
  void start() {
    engine.start();
    print("MotorCycle started");
  }
}
```
### Problems in the Previous Code:
- any change in the engine class will requires to change all other classes connected to it.
- we need only one instance of engine but in the previous code there is 3 instances of engine for each class which cause load on memory.
- if we created more than one instance of the same class like: car each time you create instance of car you will be forced to create instance of engine with it.
- صعب اختبار `Car` باستخدام **Unit Testing** لأن الكود بيخلق `Engine` جوه `Car`، فمش هنقدر نستبدله بمحرك وهمي (Mock Engine) في الاختبار.
### What if Engine become more Complex:
```dart
class Engine{
final type;
final manufacturyDate;
final manufacturingPlace;
Engine({required this.type,required this.manufacturingDate,required this.manufacturingPlace})
}
```
### Technically the problem in this Line:
```dart
Engine engine = Engine(type: ,manufacturyDate: ,manufacturingPlace: ); // this line is the problem
```
>[!TIP] > the Solution of all this problems is using Dependency Injection

