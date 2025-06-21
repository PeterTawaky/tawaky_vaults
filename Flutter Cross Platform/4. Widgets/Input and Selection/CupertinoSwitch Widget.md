> the Switch button in iPhone phones
```dart
upertinoSwitch(
  activeTrackColor: AppColors.primary,
  value: deviceModel.isOn == null
	  ? false
	  : deviceModel.isOn!
		  ? true
		  : false,
  onChanged: onChanged,
),
```