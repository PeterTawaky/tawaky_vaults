> this happens when the API bring sometimes double sometimes Integer, you can't receive this field in one of them the best solution is to use the keyword `num`

```dart
class MyModel {
  final num value;

  MyModel({required this.value});

  factory MyModel.fromJson(Map<String, dynamic> json) {
    return MyModel(value: json["value"]);
  }
}

```