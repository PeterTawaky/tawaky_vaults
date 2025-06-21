---
type: permanent
tags:
  - dart
parent: "[[Mastering Dart]]"
---
you can use Looping by **`built in methods`** in dart or you can make loops by your own hand using **`default for Loop`**.
## 1. **built in methods**
___
The primary difference between the `forEach` and `map` methods in Dart lies in their **purpose** and **return behavior**:
### 1. **Purpose**

- **`forEach`**: Used to perform an `action` for each element in the collection. It is generally used for side effects, such as printing to the console or modifying variables outside the loop.
- **`map`**: Used to `transform` the elements of a collection. It produces a new iterable where each element is the result of applying the transformation function to the corresponding element in the original collection.
### 2. **Return Value**

- **`forEach`**: Does **not** return anything (`void`). It is used solely for executing code for each element in the collection.
- **`map`**: Returns a **lazy iterable** (a `MappedIterable`) with the transformed values. You can convert it to a concrete collection like a `List` or a `Set` if needed.
___
### Examples

#### `forEach` Example
```dart
void main() {
  List<int> numbers = [1, 2, 3, 4];
  
  Map<String, dynamic> tawaky = {

    'name': 'Tawaky',

    'age': 23,

    'id': 20200067,

    'department': 'Mechatronics engineering',

  };

  // Using forEach with List
  numbers.forEach((number) {
    print('Number: $number');
  });
  //using forEach with map
  tawaky.forEach((key, value) => print('$key ----> $value'));
}

```
### `map` Example
```dart
void main() {
  List<int> numbers = [1, 2, 3, 4];
  Map<String, dynamic> tawaky = {

    'name': 'Tawaky',

    'age': 23,

    'id': 20200067,

    'department': 'Mechatronics engineering',

  };

  // Using map to transform elements
  Iterable<int> squares = numbers.map((number) => number * number);
  tawaky.map((key, value) {

    print('$key ----> $value');

    return MapEntry(key, value);

  });

  print(squares.toList()); // Converting the result to a list
}

```
___
### When to Use Which

- Use **`forEach`** for performing actions, like logging or updating variables, where you don't need a new collection.
- Use **`map`** when you need to transform a collection and create a new collection (e.g., mapping from one data type to another).

## 2. **default for Loop**
___
this way depends on which data type you will loop on **`List`** or **`Map`**:
### 1. **Looping on List**
```dart
void main() {

  List numbers = [
    1,
    2,
    3,
    4,
  ];

  for (var number in numbers) {
    number *= number;
    print(number);
  }
}

```
### 1. **Looping on Map**
```dart
void main() {

  Map<String, dynamic> tawaky = {
    'name': 'Tawaky',
    'age': 23,
    'id': 20200067,
    'department': 'Mechatronics engineering',
  };

  for (MapEntry item in tawaky.entries) {
    print('${item.key}--->${item.value}');
  }
}
```