### Reference Video:
[Flutter Local Authentication Tutorial ](https://www.youtube.com/watch?v=cYeQCGr6F7c)
### Initialization:
- download the local authentication package: [local auth](https://pub.dev/packages/local_auth)
- make it available to iOS go to the path:
	$ios/Runner/Info.plist$
	
	and add this lines in the dictionary section:
	```
	<key>NSFaceIDUsageDescription</key>
	<string>Why is my app authenticating using face id?</string>
	```
- make it available to Android go to the path:
$android/app/src/main/kotlin/tawakycreation/smart_garage_final_project/MainActivity.kt$
- replace the `FlutterActivity` with `FlutterFragmentActivity`
```
import io.flutter.embedding.android.FlutterFragmentActivity

class MainActivity : FlutterFragmentActivity()
```
then go to the path:
$android/app/src/main/AndroidManifest.xml$
add this line in manifest section:
```
  <uses-permission android:name="android.permission.USE_BIOMETRIC"/>
```
### Use in Code:
- take the package in a variable to use all it's methods:
```dart
  final LocalAuthentication auth = LocalAuthentication();
```
>[!TIP] > the only problem that  you may face is that the user can dismiss the authentication container but we can solve it by logic.
### Un Dismissible Fingerprint: 
```dart
Future<bool?> _activeFingerPrintAuth() async {
  try {
    final bool canAuthenticateWithBiometrics = await auth.canCheckBiometrics;

    if (canAuthenticateWithBiometrics) {
      bool didAuth = false;

      while (!didAuth) {
        didAuth = await auth.authenticate(
          localizedReason: 'Please authenticate Tawaky',
          options: AuthenticationOptions(
            biometricOnly: true, // Use fingerprint only
            stickyAuth: true, // Prevent authentication dismissal
          ),
        );
      }

      return didAuth;
    }
  } catch (e) {
    print(e);
  }
  return null;
}

```
### Helper Function to Navigate when user is valid:
```dart
_ensureUserValidity() async {
    final bool? userIsValid = await _activeFingerPrintAuth();
    if (userIsValid != null && userIsValid) {
      Navigator.push(
        context,
        MaterialPageRoute(builder: (context) => HomeScreen()),
      );
    }
  }
```