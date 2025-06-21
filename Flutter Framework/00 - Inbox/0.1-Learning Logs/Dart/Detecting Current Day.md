---
type: permanent
tags:
  - dart
parent: "[[Mastering Dart]]"
---
Get the current day (1-7, where Monday is 1):
```dart
void main() {
  DateTime now = DateTime.now();
  int dayNumber = now.weekday; // 1 = Monday, 7 = Sunday
  List<String> days = [
    "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"
  ];
  String dayName = days[now.weekday - 1];
  print("Day number: $dayNumber");
  print("Today is: $dayName");
}

```
### Get the full date and format it (using `intl` package)

If you want a properly formatted date with the day name:
```dart
import 'package:intl/intl.dart';

void main() {
  DateTime now = DateTime.now();
  String formattedDate = DateFormat('EEEE').format(now); // 'EEEE' gives full day name
  print("Today is: $formattedDate");
}
```