---
type: permanent
tags:
  - dart
  - OOP
parent: "[[Mastering Dart]]"
---
في **Dart**، لما تلاقي اسم دالة (أو متغير أو كلاس) بيبدأ بـ **underscore (_)** زي `_anyName`، ده معناه إن العنصر ده **خاص (private)** داخل الملف اللي هو فيه.

### 🛠️ ليه نستخدم الـ `_`؟

في **Dart**، مفيش كلمات مفتاحية زي `private` أو `protected` زي بعض اللغات التانية، لكن فيه مفهوم الـ **library privacy**، وده معناه:

- **لو الدالة أو المتغير اسمه بيبدأ بـ `_`** → مش هيكون متاح لأي كود برا الملف `.dart` اللي هو فيه.
- **لو الاسم بدون `_`** → هيكون **عام (public)** ومتقدر تستدعيه من أي مكان.

### 🔹 مثال عملي:

#### ملف `helper.dart`:
```dart
void publicFunction() {
  print("This is a public function");
}

void _privateFunction() {
  print("This is a private function");
}

```
#### ملف `main.dart`:
```dart
import 'helper.dart';

void main() {
  publicFunction(); // ✅ تشتغل عادي
  _privateFunction(); // ❌ خطأ! مش مسموح باستخدامها هنا
}

```

### 🏆 متى تستخدم `_`؟

✅ لما يكون عندك **دوال أو متغيرات مساعدة** مش محتاج حد يقدر يستخدمها خارج الملف.  
✅ لما تعمل **كلاس داخلي (Private Class)** جوه الملف، بحيث يكون استخدامه محصور داخل نفس الملف.

### ⚠️ ملاحظة:

الـ `_` بيجعل العنصر خاص بس **داخل نفس الملف**، لكنه مش بيحميه داخل الكلاس نفسه. لو عندك أكثر من كلاس في نفس الملف، يقدروا يشوفوا الدوال أو المتغيرات اللي فيها `_`.

### 📌 الخلاصة:

**`_` في Dart بيجعل العنصر خاص داخل الملف فقط، مش داخل الكلاس.** وده مفيد لتنظيم الكود ومنع الوصول غير الضروري للعناصر الداخلية. 💡
___
### 📌 **مثال على Private Class و Private Variable**

#### 📝 ملف `library.dart`
```dart
// كلاس خاص لأنه يبدأ بـ _
class _PrivateClass {
  // متغير خاص لأنه يبدأ بـ _
  String _secret = "This is a secret";

  // دالة عامة تقدر ترجّع قيمة المتغير الخاص
  String getSecret() {
    return _secret;
  }
}

// كلاس عام يقدر يتم استدعاؤه من أي مكان
class PublicClass {
  void showMessage() {
    print("This is a public class");
  }
}

```
#### 📝 ملف `main.dart`
```dart
import 'library.dart';

void main() {
  PublicClass publicObj = PublicClass();
  publicObj.showMessage(); // ✅ يشتغل عادي

  _PrivateClass privateObj = _PrivateClass(); // ❌ خطأ! مش مسموح باستخدامه
  print(privateObj._secret); // ❌ خطأ! مش مسموح بالوصول للمتغير الخاص
}

```
---

### 🔹 **شرح الكود**

1. `class _PrivateClass` → كلاس **خاص** (مش هيكون متاح خارج `library.dart`).
2. `String _secret` → متغير **خاص** داخل `_PrivateClass`، يعني مش ممكن الوصول إليه مباشرة حتى داخل نفس الملف.
3. `String getSecret()` → دالة عامة داخل `_PrivateClass`، تسمح بإرجاع قيمة `_secret` بطريقة غير مباشرة.
4. `PublicClass` → كلاس **عام**، يقدر يتم استخدامه في أي ملف.
5. `main.dart` حاول يستدعي `_PrivateClass` أو `_secret` مباشرة لكنه فشل لأنهم خاصين.
___
### ✅ **كيف يمكن الوصول للمتغير الخاص؟**

لو عايز توصل للمتغير الخاص `_secret`، لازم توفر **Getter Method** زي `getSecret()`:
```dart
void main() {
  var obj = _PrivateClass(); // ❌ خطأ! مش مسموح لأنه private
  print(obj.getSecret());    // ✅ الطريقة الصحيحة للوصول للمتغير الخاص
}
```
---

### 📌 **الخلاصة**

- أي **كلاس أو متغير أو دالة يبدأ بـ `_`** بيكون **خاص** ومش متاح خارج الملف `.dart` اللي هو فيه.
- نستخدم **Getter Methods** عشان نوصل للمتغيرات الخاصة بطريقة آمنة.
- الكلاسات العامة تفضل مفتوحة للاستخدام في أي مكان بينما الخاصة بتكون مقصورة على نفس الملف فقط.

🔹 **نصيحة**: استخدام الخصوصية في الكود بيحسن الأمان وبيخلي الكود منظم أكتر. 🚀