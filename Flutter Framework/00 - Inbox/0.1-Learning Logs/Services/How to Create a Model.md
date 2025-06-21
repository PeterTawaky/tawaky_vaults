---
tags: 
status: in Progress
parent: 
type: Permanent Note
deeper: 
against:
---
### 📌Index:
- [[How to Create a Model#📌Manually Creation]]
- [[How to Create a Model#📌Create by Extension]]
___
### 📌Manually Creation:
- any variable could have no value make it nullable (Like: image).
- if you needed to put default value make it.
- create a factory constructor `fromJson` to create model from map.
- create a `toJson` to create a Map from Model.
- for map inside a map (complex):
	- create a model for each map
	- start with the smallest one
```dart
class ElevatorModel {
  final String? userId;
  final bool available;
  final String? parkSection;

  ElevatorModel({
    required this.userId,
    required this.available,
    required this.parkSection,
  });

  factory ElevatorModel.fromJson(Map<String, dynamic> json) {
    return ElevatorModel(
      userId: json['userId'],
      available: json['available'],
      parkSection: json['parkSection'],
    );
  }

  Map<String, dynamic> toJson() {
    return {
      'userId': userId,
      'available': available,
      'parkSection': parkSection,
    };
  }
}
```
___
### 📌Create by Extension:
- download the extension: `Json to Dart Model`
- copy the map or list of maps
- `ctrl+shift+P` and `choose Json to dart from ClipBoard`
- write the name of class you need to create
- choose `equatable` package
- add copy with method to make a copy of my model
- choose the location of the model
- download the package `equatable`