1. install the extension : `flutter intl`
	
2. define it in your project:
	- `ctrl+shift+p`
	- `intl initialize`
3. install packages:
	[flutter_localization | Flutter package](https://pub.dev/packages/flutter_localization)
	[intl | Dart package](https://pub.dev/packages/intl)
1. add Languages feature to the iOS:
	- To enable localization for iOS apps, extend `ios/Runner/Info.plist` file with supported locales configuration. This list should be consistent with the locales listed in the `lib/l10n` folder.
	- write this `command` in `Info.plist` file
```
<key>CFBundleLocalizations</key>  
<array>  
<string>en</string>  
<string>ar</string>  

</array>
```
3. add the Arabic local Languages you need:
	- `ctrl+shift+p`
	- press: `intl: add locale`
	- `ar`

	> `Json` file of all language you need is created of `"key":"value"`
	
### Use Languages in your UI:
1. in `MaterialApp` : give this field
```dart
import 'package:flutter_localizations/flutter_localizations.dart';

locale: Locale('en'),  //here you can change the languge
      localizationsDelegates: const [
        S.delegate,
        GlobalMaterialLocalizations.delegate,
        GlobalWidgetsLocalizations.delegate,
        GlobalCupertinoLocalizations.delegate,
      ],
      supportedLocales: S.delegate.supportedLocales,
```
### How to access the values of `Json` in your UI through the Key:
$$S.of(context).Key$$
> [!TIP] > you should use state management to update the language through UI