>making toggle icon with the title of this toggle
```dart
	SwitchListTile(
		title: //accept text widget
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
> [!TIP] > you c an control it's size by putting it in container