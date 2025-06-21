---
type: permanent
tags:
  - dart
parent: "[[Mastering Dart]]"
---
### Basic Use: as a set of Constant Values: 
#### using class:
```dart
class Constants{
static String processing="Processing";
static String inTransit="In Transit";
static String delivered="Delivered";
}
```
### Using Enum is the best:
```dart
enum OrderStatus {
  processing,
  inTransit,
  delivered;

  String get humanReadableName {
    switch (this) {
      case OrderStatus.processing:
        return 'Processing';
      case OrderStatus.inTransit:
        return 'In Transit';
      case OrderStatus.delivered:
        return 'Delivered';
    }
  }
}
```
___
### Enhanced Enum:
 
 >[!ERROR] >to be completed later... 
 
 ___
 > قيم ثابتة أو متغيرات تندرج تحت title واحد.
> define named constant values

في لغة **Dart**، الكلمة المفتاحية `enum` تُستخدم لتعريف **تعداد (Enumeration)**، وهو نوع بيانات مخصص يُستخدم لتمثيل مجموعة ثابتة من القيم المرتبطة ببعضها. التعدادات مفيدة عند التعامل مع قيم ثابتة يمكن تحديدها مسبقًا، مثل أيام الأسبوع، ألوان، أو حالات معينة في التطبيق.

---

## **إنشاء `Enum` في Dart**
الصيغة الأساسية لتعريف `enum` هي:
```dart
enum EnumName {
  value1,
  value2,
  value3,
}
```
### **مثال عملي**
```dart
enum Days {
  Sunday,
  Monday,
  Tuesday,
  Wednesday,
  Thursday,
  Friday,
  Saturday
}
```
الآن، يمكننا استخدام التعداد `Days` في الكود:
```dart
void main() {
  Days today = Days.Monday;
  print(today); // Days.Monday
}
```
---

## **خصائص واستخدامات `enum`**

### **1. الحصول على جميع القيم داخل `enum`**

يمكنك استخدام `values` للحصول على **قائمة** بجميع القيم داخل التعداد:
```dart
void main() {
  print(Days.values);
  // [Days.Sunday, Days.Monday, Days.Tuesday, Days.Wednesday, Days.Thursday, Days.Friday, Days.Saturday]
}
```
### **2. استخدام التعداد مع `switch`**
```dart
void checkDay(Days day) {
  switch (day) {
    case Days.Sunday:
      print("Today is Sunday, it's a weekend!");
      break;
    case Days.Monday:
      print("Back to work!");
      break;
    default:
      print("It's a regular day.");
  }
}

void main() {
  checkDay(Days.Sunday);
}
```
___
> ابتداءً من **Dart 2.17**، يمكن للتعدادات أن تحتوي على **خصائص ودوال**، مما يجعلها أكثر قوة.
### Examples for things need `enum`:
1. Sizes
2. Network Errors
3. Languages
4. screens

```dart
enum Size {
  SMALL('small'),
  MEDIUM('medium'),
  LARGE('large');
  final String choosedSize;
  const Size(this.choosedSize);
}

  
enum ClientNetworkError {
  //each item must have error the two fields
  badRequest(400, 'this is a bad request'),
  unAuthorized(401, 'this is an unauthorized access'),
  paymentRequired(402, 'there is a required payment'),
  forbidden(403, 'access forbidden'),
  notFound(404, 'Not found');

//like class body
  final int errorNumber;
  final String errorMsg;
  const ClientNetworkError(this.errorNumber, this.errorMsg);
}

void main() {
  print(ClientNetworkError.values.map((error) => error.errorNumber));
  print(ClientNetworkError.values.map((error) => error.errorMsg));
}
```
___
```dart
enum Colors {
  red(0xFF0000),
  green(0x00FF00),
  blue(0x0000FF);

  final int hexCode;

  const Colors(this.hexCode);

  void printColor() {
    print('The color code for $name is $hexCode');
  }
}

void main() {
  Colors myColor = Colors.green;
  myColor.printColor(); // The color code for green is 65280
}
```
## **استخدام `enum` مع `index`**

كل عنصر في `enum` لديه **فهرس (Index) يبدأ من 0**.
```dart
void main() {
  print(Days.Sunday.index);   // 0
  print(Days.Wednesday.index); // 3
}
```
## **متى نستخدم `enum`؟**

- عندما يكون لديك **مجموعة ثابتة من القيم** مثل أيام الأسبوع، حالات الطلب، أو ألوان.
- لتجنب استخدام **قيم نصية أو أرقام عشوائية** قد تؤدي إلى أخطاء.
- عند الحاجة إلى **توفير وظائف إضافية داخل التعداد** مثل تخزين القيم أو الدوال المساعدة.

---

## **الخلاصة**

- `enum` في Dart يُستخدم لإنشاء **مجموعة من القيم الثابتة**.
- يمكن الوصول إلى جميع القيم باستخدام `values`.
- يدعم `switch` لتسهيل التعامل مع الحالات المختلفة.
- ابتداءً من Dart 2.17، يمكن إضافة **خصائص ودوال** داخل `enum`.
- يمكن استخدام `extension` لإضافة وظائف إضافية دون تعديل `enum` نفسه.
- يمكن تحويل `enum` إلى `String` والعكس باستخدام `name` و `firstWhere`.