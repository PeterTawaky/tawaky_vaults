> Control the Place of it's child widget

```dart
Align(
  alignment: Alignment.bottomRight,
  child: MaterialButton(
	  color: Colors.red,
	  child: Text('Add Data'),
	  onPressed: () {
		Navigator.pop(context);
	  }),
)
```
