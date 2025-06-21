---
tags:
  - dart
parent: 
type: Permanent Note
deeper: 
against:
---
The `trim()` function in Dart is used to **remove all leading and trailing whitespace** from a string. This includes spaces, tabs, and newline characters at the beginning and end of the string, but **not** the whitespace in the middle.

### Example:
```dart
void main() {
  String raw = '   Hello, Dart!   ';
  String trimmed = raw.trim();

  print('Before trim: "$raw"');
  print('After trim: "$trimmed"');
}
```
### Output:
```
Before trim: "   Hello, Dart!   "
After trim: "Hello, Dart!"
```
### Most Used:
with email and password before sending it to the database.