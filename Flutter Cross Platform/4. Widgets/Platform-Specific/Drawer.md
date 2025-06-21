
## How to Open Drawer by Function with any button:
#### Way 1:
```dart
Scaffold.of(context).openDrawer();
```
>[!Note] the widget that will use this command should be wrapped with Builder Widget

#### Way 2:
- create a global key to the scaffold
```dart
    GlobalKey<ScaffoldState> _scaffoldKey = GlobalKey<ScaffoldState>();
```
- use it in the Scaffold():
```dart
Scaffold(
  key: _scaffoldKey, // تعيين المفتاح للـ Scaffold
)
```
- use this command in the widget:
```dart
 _scaffoldKey.currentState?.openDrawer(); // استخدام المفتاح لفتح الدروير
```