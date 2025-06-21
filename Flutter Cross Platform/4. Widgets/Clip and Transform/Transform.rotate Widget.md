> can rotate any basic widget with the degree you want.

```dart
Transform.rotate(
	angle: pi * 1.5, // 270 degree //from math library
	child: CupertinoSwitch(
		activeTrackColor: AppColors.primary,
		value: deviceModel.isOn == null
			? false
			: deviceModel.isOn!
				? true
				: false,
		onChanged: onChanged),
  ),
```
### Rotate Degrees:
1. pi   (180 degree)
2. pi * 1.5 (270 degree)
3. pi/2     (90 degree)