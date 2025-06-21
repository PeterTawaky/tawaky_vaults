>making the toggle icon
```dart
	Switch(
		//create a boolean status variable to toggle between values
		value: status,
		activeTrackColor:
		activeColor:
		inactiveTrackColor:
		inactiveThumbColor:
		onChanged: (choosenValue) {
		  setState(() {
			status = choosenValue;
		  });
		},
    ),

```
