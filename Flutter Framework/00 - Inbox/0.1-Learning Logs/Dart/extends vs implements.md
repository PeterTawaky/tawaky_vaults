---
type: permanent
tags:
  - dart
  - OOP
parent: "[[Mastering Dart]]"
---
Both `implements` and `extends` are used in **object-oriented programming (OOP)** in Dart, but they serve different purposes when working with classes and inheritance.

---

## **1️⃣ `extends` → Inheritance (Single)**

The `extends` keyword is used for **class inheritance**, allowing a subclass to inherit:  
✅ **Properties (fields)**  
✅ **Methods (functions)**  
✅ **Constructors (with conditions)**

🔹 The child class **inherits everything from the parent class** and can **override** methods.  
🔹 Dart **only supports single inheritance**, so a class **can extend only one class**.

### **Example of `extends`**
```dart
class Animal {
  void makeSound() {
    print("Animal makes a sound");
  }
}

class Dog extends Animal {
  @override
  void makeSound() {
    print("Dog barks");
  }
}

void main() {
  Dog dog = Dog();
  dog.makeSound(); // Dog barks
}
```
✔ **`Dog` inherits `makeSound` from `Animal` and overrides it.**  
✔ **It can access `Animal`'s properties and methods directly.**

---

## **2️⃣ `implements` → Interface-Like Behavior (Multiple)**

The `implements` keyword is used to **force a class to provide its own implementation of all methods and properties** from another class or interface.

🔹 **Does NOT inherit implementation**—it only forces the child class to define all methods.  
🔹 Unlike `extends`, Dart allows a class to **implement multiple classes**.

### **Example of `implements`**
```dart
class Animal {
  void makeSound() {
    print("Animal makes a sound");
  }
}

class Dog implements Animal {
  @override
  void makeSound() {
    print("Dog barks");
  }
}

void main() {
  Dog dog = Dog();
  dog.makeSound(); // Dog barks
}
```
✔ **`Dog` implements `Animal`, but does not inherit from it.**  
✔ **The method `makeSound` must be explicitly implemented.**

---

## **3️⃣ Key Differences Between `extends` and `implements`**

|Feature|`extends` (Inheritance)|`implements` (Interface)|
|---|---|---|
|Inherits properties/methods?|✅ Yes|❌ No (must redefine everything)|
|Can override methods?|✅ Yes (optional)|✅ Yes (mandatory)|
|Can inherit constructors?|✅ Yes|❌ No|
|Supports multiple classes?|❌ No (only one class)|✅ Yes (multiple interfaces)|
|Forces method implementation?|❌ No|✅ Yes (must implement all methods)|

---

## **4️⃣ Example: `extends` vs `implements`**

Let's define an `Animal` class and see how `extends` and `implements` behave differently.
```dart
class Animal {
  void eat() {
    print("Animal is eating");
  }
}

class Dog extends Animal {
  // Dog inherits the eat() method from Animal
}

class Cat implements Animal {
  @override
  void eat() {
    print("Cat is eating");
  }
}

void main() {
  Dog dog = Dog();
  dog.eat(); // Inherited: "Animal is eating"

  Cat cat = Cat();
  cat.eat(); // Must override: "Cat is eating"
}
```
✔ **`Dog` automatically inherits `eat()` without redefining it.**  
✔ **`Cat` MUST implement `eat()` since `implements` does not inherit anything.**

---

## **5️⃣ `extends` vs `implements` with Multiple Classes**

Since Dart **does not support multiple inheritance (`extends`)**, we use `implements` to achieve it.

### **Example: Multiple `implements`**
```dart
class Animal {
  void makeSound();
}

class CanFly {
  void fly();
}

class Bird implements Animal, CanFly {
  @override
  void makeSound() {
    print("Bird chirps");
  }

  @override
  void fly() {
    print("Bird is flying");
  }
}

void main() {
  Bird bird = Bird();
  bird.makeSound(); // Bird chirps
  bird.fly();       // Bird is flying
}
```
✔ **`Bird` implements multiple classes but must redefine all methods.**  
✔ **We achieve multiple inheritance behavior using `implements`.**

---

## **6️⃣ When to Use `extends` vs `implements`?**

✅ **Use `extends` when:**

- You want to **inherit** properties/methods from a parent class.
- You want to **override only some** methods, not all.
- You are building a **hierarchy** (e.g., `Animal -> Dog`).

✅ **Use `implements` when:**

- You need **multiple inheritance** (since `extends` supports only one parent).
- You want to enforce **interface-like behavior**, where every method must be defined.
- You want to **design flexible contracts** for classes.

---

### **🔹 Final Thought**

- `extends` = **inherits and can override** methods and properties.
- `implements` = **must override everything, does not inherit any implementation**.
- Use `extends` for **hierarchy** and `implements` for **multiple inheritance-like behavior**.