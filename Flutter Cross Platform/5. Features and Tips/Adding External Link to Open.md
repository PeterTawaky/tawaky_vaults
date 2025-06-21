- download the Package: [url-launcher | Flutter package](https://pub.dev/packages/url_launcher)
- choose the URL schemes according to the link you are going to
	- https
	- mailto
	- tel
	- sms
	- file
- Add Configurations for iOS
- Add Configurations for Android
- integrate code with flutter
### iOS:
	in info.plist
```
<key>LSApplicationQueriesSchemes</key>
<array>
  <string>sms</string>
  <string>tel</string>
  <string>https</string>
</array>
```
### Android:
```xml
<!-- Provide required visibility configuration for API level 30 and above -->
<queries>
  <!-- If your app checks for https support -->
  <intent>
    <action android:name="android.intent.action.VIEW" />
    <data android:scheme="https" />
  </intent>
  <!-- If your app checks for call support -->
  <intent>
    <action android:name="android.intent.action.VIEW" />
    <data android:scheme="tel" />
  </intent>
  <!-- If your application checks for inAppBrowserView launch mode support -->
  <intent>
    <action android:name="android.support.customtabs.action.CustomTabsService" />
  </intent>
</queries>
```
### Integrate Code with Flutter:
```dart
import 'package:flutter/material.dart';
import 'package:url_launcher/url_launcher.dart';

final Uri _url = Uri.parse('https://flutter.dev');

void main() => runApp(
      const MaterialApp(
        home: Material(
          child: Center(
            child: ElevatedButton(
              onPressed: _launchUrl,
              child: Text('Show Flutter homepage'),
            ),
          ),
        ),
      ),
    );

Future<void> _launchUrl() async {
  if (!await launchUrl(_url)) {
    throw Exception('Could not launch $_url');
  }
}
```