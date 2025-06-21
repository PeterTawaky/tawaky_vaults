---
type: permanent
tags:
  - dart
  - OOP
parent: "[[Mastering Dart]]"
---
### **Difference Between `sealed class` and `abstract class` in Dart**

Both `sealed class` and `abstract class` are used to define **base classes** that are not meant to be instantiated directly, but they serve different purposes.

---

## **1️⃣ Sealed Class (`sealed class`)**

A **sealed class** in Dart:

- **Can only be extended inside the same library (file).**
- **Cannot be implemented (`implements`) by other classes.**
- Helps the compiler **exhaustively check cases** in a `switch` statement.
- Is useful for **state management** and defining **strict hierarchies**.

### **Example of `sealed class`**
```dart
sealed class Animal {}

class Dog extends Animal {}
class Cat extends Animal {}

// This will cause an error if it's in another file:
// class Lion extends Animal {} ❌

```
✅ **Ensures that only `Dog` and `Cat` can extend `Animal`, keeping hierarchy controlled.**

---

## **2️⃣ Abstract Class (`abstract class`)**

An **abstract class** in Dart:

- Can be **extended (`extends`) or implemented (`implements`) anywhere**, even outside the library.
- **Can have abstract or concrete methods**.
- **Does NOT enforce strict hierarchies**, meaning other files can create subclasses.

### **Example of `abstract class`**
```dart
abstract class Vehicle {
  void move(); // Abstract method
}

class Car extends Vehicle {
  @override
  void move() {
    print("Car is moving");
  }
}

class Bike implements Vehicle {
  @override
  void move() {
    print("Bike is moving");
  }
}
```
✅ **Can be extended or implemented anywhere, making it more flexible.**

---

## **🆚 Key Differences Between `sealed class` and `abstract class`**

|Feature|**Sealed Class (`sealed`)**|**Abstract Class (`abstract`)**|
|---|---|---|
|**Can be extended (`extends`)**|✅ Yes, but only inside the same file|✅ Yes, from any file|
|**Can be implemented (`implements`)**|❌ No|✅ Yes|
|**Restricts subclassing?**|✅ Yes, within the same file|❌ No, any file can extend it|
|**Forces exhaustive `switch`?**|✅ Yes (compiler enforces all cases)|❌ No|
|**Has abstract methods?**|❌ Not necessary|✅ Yes, can contain abstract methods|
|**Best Use Case**|**When you need a strict hierarchy (e.g., state management, event handling).**|**When you want to allow other classes to implement/extend freely.**|

---

## **When to Use `sealed class` vs `abstract class`?**

### ✅ **Use `sealed class` when:**

- You **want full control over subclasses** and **prevent others from extending it** outside the file.
- You **want `switch` to enforce exhaustive cases**.
- You're working on **state management** (e.g., Bloc, Riverpod).

### ✅ **Use `abstract class` when:**

- You **want other files to extend or implement it freely**.
- You need **a base class with abstract methods** for multiple implementations.
- You're designing **interfaces** or **common behaviors**.
## **Final Thought**

Use `sealed class` when you need **strict control** over subclassing and `abstract class` when you need **flexibility**.

🔹 **If you're building a class hierarchy where you don't want external files to extend it → Use `sealed class`.**  
🔹 **If you want an abstract blueprint that can be extended anywhere → Use `abstract class`.**