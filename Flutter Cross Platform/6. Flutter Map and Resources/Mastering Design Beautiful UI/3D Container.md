## Resources:
[Clickable-3d-Container](https://youtu.be/A2Bbhr3DGd0?si=WHY_5qVeuGShnfEH)
[3d-Container](https://youtu.be/X47zIAGIJNE?si=rRShDYqDjC5BARvP)
## Tips:
- give the container the color of the background : 
- create two box shadow one for dark and the other for white colors:
```dart
Color? containerColor = isDarkMode ? Color(0XFF2E3239) : Colors.grey[300];
boxShadow: [
  BoxShadow(
	// تغميق
	color:
		isDarkMode ? Color(0XFF23262A) : Colors.grey.shade500,
	offset: Offset(10, 10),
	blurRadius: 15,
	spreadRadius: 1,
  ),
  BoxShadow(
	//تفتيح
	color: isDarkMode ? Color(0XFF35393F) : Colors.white,
	offset: Offset(-10, -10),
	blurRadius: 15,
	spreadRadius: 1,
  ),
]
```
