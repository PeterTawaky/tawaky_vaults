---
tags: 
parent: 
type: Permanent Note
deeper: 
against:
---
### Index:
[[Abstract Class#📌Intro]]
[[Abstract Class#📌Abstract Function]]
[[Abstract Class#📌Abstract vs Private Class]]
[[Abstract Class#📌Abstract Kills switch-`enum`]]
___
### 📌Intro:
**abstract class** is a class that **cannot be directly used to create objects**, and is meant to be **inherited by other classes**. It can have **abstract methods** (without code) and **regular methods** (with code).
#### Why to Use:
**Create a common base** for other classes, where we can **define shared features** and **force child classes** to complete the missing parts (like abstract methods).
___
### 📌Abstract Function:
>دالة يتم تعريفها داخل **class abstract** ولكن بدون تنفيذ (body). الهدف منها هو إلزام أي **class** يرث هذه **abstract class** بتنفيذ (override) هذه الدالة.

#### When to Use:
نستخدمها عندما يكون لدينا **كلاس أب (Parent Class)** يمثل مفهومًا عامًا، ونريد أن نجبر أي **كلاس ابن (Child Class)** يرثه على تنفيذ دالة معينة ولكن بطريقة خاصة به.
#### How to Use:
- يجب أن تكون داخل **abstract class**.
- لا تحتوي على **body** (تنفيذ).
- يتم تعريفها باستخدام **;** بدلًا من `{}`.
```dart
abstract class Animal {
  void makeSound(); // دالة مجردة (abstract function)
}

class Dog extends Animal {
  @override
  void makeSound() {
    print("Woof! Woof!");
  }
}

class Cat extends Animal {
  @override
  void makeSound() {
    print("Meow! Meow!");
  }
}

void main() {
  Dog dog = Dog();
  dog.makeSound(); // Woof! Woof!

  Cat cat = Cat();
  cat.makeSound(); // Meow! Meow!
}

```
#### Summary:
- **الـ abstract function** هي دالة بدون تنفيذ تُعرّف داخل **abstract class**.
- **أي class يرث الـ abstract class يجب أن ينفذ جميع الـ abstract functions** وإلا يجب أن يكون abstract هو الآخر.
- **تستخدم لتحديد سلوكيات مشتركة وإجبار الكلاسات الأبناء على تنفيذها بطريقتها الخاصة**.
___
### 📌Abstract vs Private Class:
| **الميزة**                                | **private constructor**                                 | **abstract class**                                     |
| ----------------------------------------- | ------------------------------------------------------- | ------------------------------------------------------ |
| إمكانية إنشاء كائن منه                    | ❌ لا يمكن (إلا داخل نفس الملف)                          | ❌ لا يمكن                                              |
| هل يمكنه احتواء دوال؟ (Functions)         | ✅ نعم، لكن يجب أن تكون `static` إذا كان `Utility Class` | ✅ نعم، يمكن أن يحتوي على دوال عادية ودوال مجردة        |
| هل يمكنه أن يكون Base Class؟              | ❌ لا، لا يمكن الوراثة منه (`extends`)                   | ✅ نعم، يمكن استخدامه كأساس لكلاسات أخرى                |
| هل يجبر الكلاسات الأخرى على تنفيذ الدوال؟ | ❌ لا                                                    | ✅ نعم، يجبر الكلاسات المتفرعة على تنفيذ الدوال المجردة |

---

## **📝 متى تستخدم كل واحد؟**

✅ **استخدم `private constructor` إذا كنت تريد منع إنشاء الكائنات**، مثل `Singleton` أو `Utility Classes`.  
✅ **استخدم `abstract class` إذا كنت تريد إنشاء كلاس أساسي (Base Class) يحتوي على دوال يجب تنفيذها** في الكلاسات التي ترث منه.
🚀 **الخلاصة:**

- **`private constructor`** يمنع إنشاء الكائنات لكنه لا يمنع الوراثة.
- **`abstract class`** يمنع إنشاء الكائنات لكنه يسمح بالكلاسات الأخرى أن ترث منه وتنفذ دواله المجردة.
___
### 📌Abstract Kills switch-`enum`:
#### Use of if with `enum`:
>[!Important] >the code is not readable not maintainable, logic can be very large in each bloc

```dart
enum users {
  admin,
  marketing,
  sales,
  customer,
  driver,
  guestUser,
  support,
  manager,
}
```
```dart
import 'enum_users.dart';
void main() {
  getUserType(users.marketing);
}

void getUserType(users user) {
  switch (user) {
    case users.admin:
      print("Admin");
      break;
    case users.marketing:
      print("Marketing");
      break;
    case users.sales:
      print("Sales");
      break;
    case users.customer:
      print("Customer");
      break;
    case users.driver:
      print("Driver");
      break;
    case users.guestUser:
      print("Guest User");
      break;
    case users.manager:
      print("Manager");
      break;
    case users.support:
      print("Support");
  }
}
```
#### Use abstract class for the same case:
>[!ERROR] to be completed...



