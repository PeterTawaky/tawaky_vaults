___
- user the function `runApp` instead of writing the whole code in the main function
- it's parameter should be widget so `MyApp` should extend Widget
- make the whole app render one time when it's ready not part by part
```dart
void main(){
	runApp(MyApp());
}
```