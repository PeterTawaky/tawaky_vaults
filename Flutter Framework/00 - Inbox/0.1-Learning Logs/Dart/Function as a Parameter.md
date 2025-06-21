---
type: permanent
tags:
  - dart
parent: "[[Mastering Dart]]"
---
```dart
void main() {
  math(number: 5, calculation: plus);
}
  //data type called Function
void math({required int number, required Function calculation}) {
  print(calculation(number));
}
  
int plus(int i) {
  return i + i;
}

int power(int i) {
  return i * i;
}
```