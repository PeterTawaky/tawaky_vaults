---
tags:
  - dart
  - api
parent: "[[Mastering Dart]]"
type: Permanent Note
deeper: 
against: 
---
through built-in Dart Class: Date-Time Object
### What is the date time formatted string?
a way of writing date in Data bases which found in the form of String it can be many forms.
- when we get this date from API we need to deal with it like date not like String.
	- year
	- month
	- day
	- hour
	- minute
	- second
- make some operations on this date.
### How to make a Date-Time-Object
```dart
DateTime newForm = DateTime.parse('time-formated-string'); 
```
### Deal with this object to get any data or make operations:
```dart
newForm.hour //view hour
newForm.minute //view minute
```
### Best Practice with API:
	when you get data in the model
- take the data in a variable of type `DateTime` instead of String:
```dart
final DateTime date;
```
- apply the functionality in the named constructor:
```dart
date: DateTime.parse(json[datePath]);
```