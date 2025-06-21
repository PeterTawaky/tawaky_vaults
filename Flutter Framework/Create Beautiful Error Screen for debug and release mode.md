---
tags: 
status: 
parent: 
type: Permanent Note
deeper: 
against:
---
### How to Access the Error Widget in Flutter:
	inside the make function:
```dart
ErrorWidget.builder =
      (FlutterErrorDetails details) => ModernErrorScreen(errorDetails: details);
```
### How Through an Error to Show Error Screen:
	inside the build function:
```dart
throw UnimplementedError();
```
### Build the Widget you want to appear in error case...
