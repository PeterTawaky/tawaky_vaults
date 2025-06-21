---
type: permanent
tags:
  - dart
parent: "[[Mastering Dart]]"
---
Initializing Variables
1. Normal Variable
```dart
String s='A';
//can't be null duting initiallize
//can't be null during call
```
2. Nullable Variable
```dart
String? s= null;
//can be null duting initiallize
//can be null during call
```
3. [[Late Variable]]
```dart
late String s= null;
//can be null during initiallize 
//can't be null during cal
```
Late:
مش بت create الvariable غير لما بتستخدمه فعليا, تعمله call بالتالي بتوفر مكان في memory