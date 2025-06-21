---
tags: 
parent: 
type: Permanent Note
deeper: 
against:
---
### Index:
[[Dart Keywords#📌Static Keyword]]
[[Dart Keywords#📌Late Keyword]]
[[Dart Keywords#📌`const` vs final]]
[[Dart Keywords#📌await vs then]]
___
### 📌Static Keyword:
	one variable only for all who is using this variable
#### static variable:
1. shared across all instances of a class.
2. initialized only once when the class is loaded, not each time an instance is created.
3. access a static variable using the class name without needing to create object from it.
4. if it's assigned in some place with value, this value will be general for each time you access this variable
```dart
class MyClass {
  static int counter = 0;
  
  void incrementCounter() {
    counter++;
  }
}

void main() {
  MyClass.counter = 5; // Access without creating an instance
  print(MyClass.counter); // Output: 5
  MyClass obj1 = MyClass();
  obj1.incrementCounter();
  print(MyClass.counter); // Output: 6
}

```
#### Static Function:
	the same thing function that i can call it directly from the class without any need to create an object from the class
#### 📃Best Practice of Use:
- data that need to be accessed in all the application with the same value
- with private constructor for all constants:
	- colors
	- strings
	- sizes
___
### 📌Late Keyword:
variable will take it's value in runtime
In Dart, a `late` variable is a special modifier used to declare variables that are initialized at a later point but are guaranteed to be initialized before being accessed. If a `late` variable is not initialized before being accessed, the program will throw a **`LateInitializationError`** at runtime.

### Key Points about `late` variables:

1. **Not Initialized:** A `late` variable does not have a default value, unlike regular nullable variables which default to `null` for reference types.
2. **Initialization Required Before Access:** If you try to access a `late` variable without initializing it, you will encounter a `LateInitializationError`.
3. **Use Case:** `late` is useful for scenarios where you need to defer initialization but still want the performance benefits of non-nullable types.
___
### 📌`const` vs final:
#### Key Differences:

| Feature                 | `final`                                 | `const`                                |
| ----------------------- | --------------------------------------- | -------------------------------------- |
| **Initialization**      | Can be initialized later                | Must be initialized at declaration     |
| **Value Determination** | Runtime                                 | Compile-time                           |
| **Usage**               | When value is not known at compile time | When value is known at compile time    |
| **Memory**              | Each instance can have different values | Same value shared across all instances |
___
### 📌await vs then:
> both of them used in asynchronous operations

#### Main Difference:
#### - await: 
stop all the code after it until the function is done first.
#### - then:
stop only the body of it , but the code after it will not wait until it's done.
```dart
void main() async {
  print(await delay());
  print('after delay');  //will not be printed until await delay is completed
  delay().then((value) => print(value)); //this will be delayed four seconds
  print('before delay');  //will be printed without waiting then
}
Future<String> delay() {
  return Future.delayed(Duration(seconds: 2), () => 'delayed two seconds');
}
/*  
Summary:
  by using await all program after await will be delayed until await is completed
  but in then the program after it will not be delayed
 */
```

### **الفرق الأساسي بين `await` و `then`**

|`await`|`then`|
|---|---|
|بيوقف تنفيذ الكود مؤقتًا حتى ينتهي الـ `Future`|لا يوقف تنفيذ الكود|
|يجعل الكود أكثر وضوحًا وسهولة في القراءة|يؤدي إلى تداخل الكود (Callback Hell أحيانًا)|
|يتطلب أن تكون الدالة `async`|يمكن استخدامه في أي مكان|

### **متى تستخدم كل واحد؟**

- استخدم `await` لو كنت تكتب كودًا متسلسلًا وواضحًا.
- استخدم `then` لو كنت تتعامل مع Futures داخل دوال ليست `async` أو في حالة السلاسل المتعددة من Futures.
___
