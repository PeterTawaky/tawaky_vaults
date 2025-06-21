> prevent user from auto rotate app if your app is not designed for this case.

- write this command in the main function
```dart
void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await SystemChrome.setPreferredOrientations([DeviceOrientation.portraitUp]);
  runApp(HabitTracker());
}
```