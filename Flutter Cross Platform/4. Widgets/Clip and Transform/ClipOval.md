> making Circle image of different forms.

- `svg` image:
```dart
ClipOval(
	child: SizedBox(
	  width: 100, 
	  height: 100,
	  child: SvgPicture.asset(
		'assets/tawaky.svg', // Path to your SVG file
		fit: BoxFit.cover, // Ensure the image covers the circular area
	  ),
	),
  ),
```