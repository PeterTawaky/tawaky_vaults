```dart
Checkbox(
	activeColor: AppColors.kPurple,
	shape: RoundedRectangleBorder(  //make it more rounded
		borderRadius: BorderRadius.circular(5)),
	value: state.isChecked,
	onChanged: (_) {
	  cubit.checkUncheckMark();
})
```
### How to Control the size of the chckbox:
```dart
Transform.scale(
  scale: 1.5, // Increase or decrease the size
  child: Checkbox(
    value: true,
    onChanged: (bool? value) {},
  ),
)
```