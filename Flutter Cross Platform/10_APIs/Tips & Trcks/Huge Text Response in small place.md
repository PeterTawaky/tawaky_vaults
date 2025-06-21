> if the response contains many words and you only have a small space you need only to view only some words not all, you can convert the `String response` to a `list` by `split` function and then choose the amount of words you need to view.

### Solve by number of words:  (recommended)
```dart
String? getFirstTwoWords(String? text) {
  if (text == null) return null;
  if (text.isEmpty) return null;
  List<String> words = text.split(' '); // Split by space
  if (words.length >= 2) {
    return '${words[0]} ${words[1]}'; // Take first two words
  } else {
    return text; // If less than two words, return the original string
  }
}
```
### Solve by number of characters:
```dart
Text(product.title.substring(0, 20))
```