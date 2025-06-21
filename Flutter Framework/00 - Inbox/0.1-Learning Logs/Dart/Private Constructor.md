---
type: permanent
tags:
  - dart
  - OOP
parent: "[[Mastering Dart]]"
---
> حيث لا يمكن استدعاؤه من خارج الملف (Dart file) الذي تم تعريفه فيه. يتم جعل الـ constructor خاصًا عن طريق وضع **underscore (_)** قبل اسم الـ constructor.

### Example of Uses in Flutter:
- Saving Images Strings file.
- Saving Colors Strings file.
- Saving Base URL of API Strings file.
### Why to Use:
1. **منع إنشاء كائنات من الكلاس** من خارج الكلاس نفسه.
2. **تطبيق نمط Singleton** حيث نريد التأكد من أنه لا يوجد سوى **كائن واحد فقط** من الكلاس.
3. **إخفاء منطق معين** داخل الملف وعدم السماح باستخدامه من ملفات أخرى.

---

### مثال على **private constructor**:
```dart
class MyClass {
  // Private Constructor
  MyClass._();

  void sayHello() {
    print("Hello from MyClass");
  }
}

void main() {
  // MyClass instance = MyClass(); // ❌ سيؤدي إلى خطأ لأنه private
  // لا يمكن إنشاء كائن مباشرة لأنه private
}

```
في المثال السابق، لا يمكن إنشاء كائن من `MyClass` خارج الملف لأن الـ **constructor** معرف بـ `_()` مما يجعله **خاصًا**.

---

### **استخدام الـ private constructor في نمط Singleton**

إذا أردنا تطبيق **نمط Singleton** بحيث يكون هناك **كائن واحد فقط** من الكلاس طوال وقت تشغيل التطبيق، يمكننا استخدام **private constructor** مع متغير ثابت `static`:
```dart
class Singleton {
  // إنشاء كائن ثابت من الكلاس
  static final Singleton _instance = Singleton._internal();

  // Private Constructor
  Singleton._internal();

  // دالة ترجع نفس الكائن في كل مرة
  factory Singleton() {
    return _instance;
  }

  void showMessage() {
    print("This is a Singleton class!");
  }
}

void main() {
  var obj1 = Singleton();
  var obj2 = Singleton();

  obj1.showMessage();

  print(obj1 == obj2); // ✅ سترجع true لأنهما نفس الكائن
}

```

🔹 هنا `Singleton._internal();` هو **private constructor**، و `factory Singleton()` تضمن إرجاع نفس الكائن `Singleton._instance` كل مرة.

---

## When to Use

✅ عندما تحتاج إلى **منع إنشاء كائنات من الكلاس مباشرة**.  
✅ عند تطبيق **نمط Singleton**.  
✅ عندما تريد أن يكون الكلاس مجرد **مجموعة من الدوال الثابتة (Utility Class)**.

---

### **مثال على استخدامه في Utility Class**
```dart
class Utils {
  // منع إنشاء كائنات من هذا الكلاس
  Utils._();

  static String formatText(String text) {
    return text.toUpperCase();
  }
}

void main() {
  print(Utils.formatText("hello")); // HELLO
}

```

في هذا المثال، `Utils._();` يمنع إنشاء كائنات من `Utils`، مما يجعل جميع الدوال فيه **static فقط**.

---

### Summarry:

- **private constructor** يُستخدم لمنع إنشاء كائنات من الكلاس خارج الملف.
- يُستخدم في **Singleton pattern** لضمان وجود **كائن واحد فقط**.
- مفيد في **Utility Classes** التي لا تحتاج إلى كائنات، بل فقط دوال `static`.
