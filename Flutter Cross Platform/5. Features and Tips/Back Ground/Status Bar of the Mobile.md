**الوضعيات المتاحة في `SystemUiMode`:**

- `SystemUiMode.immersive`: يخفي شريطي الحالة والتنقل ولكن يظهر عند السحب.
- `SystemUiMode.immersiveSticky`:Hides both the status bar and navigation bar, providing a full-screen experience. The overlays can temporarily reappear with a swipe
- `SystemUiMode.leanBack`: يخفي الشريطين ويظهر عند الضغط على الشاشة.
- `SystemUiMode.edgeToEdge`: يظهر الشريطين لكن يجعل المحتوى يمتد تحتهما.
- `SystemUiMode.manual`: يسمح لك بتحديد `overlays` يدويًا.

## How to Hide Status Bar and Navigation bar:
```dart
void main()  {

	WidgetsFlutterBinding.ensureInitialized();

	SystemChrome.setEnabledSystemUIMode(SystemUiMode.immersiveSticky); //hide status bar

	runApp(NewsApp());

}
```
## How to Hide Status Bar but Keep Navigation bar:
```dart
void main() {
	SystemChrome.setEnabledSystemUIMode(SystemUiMode.manual, overlays: [ 
		SystemUiOverlay.bottom, // Show navigation bar 
	]);  
	runApp(MyApp());  
}
```
## How to Change the Color of Status bar:
