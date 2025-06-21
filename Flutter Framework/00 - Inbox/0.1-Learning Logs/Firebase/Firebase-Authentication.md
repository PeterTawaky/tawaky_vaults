---
tags:
  - BaaS
  - fire-base
parent: "[[Intro to Firebase]]"
type: Permanent Note
deeper: 
against:
---
### Index:
[[Firebase-Authentication#📌Documentation]]
[[Firebase-Authentication#📌Set up the Work Environment]]
[[Firebase-Authentication#📌Different Sign-in Methods]]
[[Firebase-Authentication#📌Tips and Tricks]]
[[Firebase-Authentication#📌Social Authentication]]
[[Firebase-Authentication#📌Snippet Code]]
[[Firebase-Authentication#📌Another Concepts need to Cover]]

___
### 📌Documentation:
[Firebase Authentication on Flutter | FlutterFire](https://firebase.flutter.dev/docs/auth/start/)
___
### 📌Set up the Work Environment:
#### ⛏Activate Authentication Feature via Firebase Project | [authentication](https://console.firebase.google.com/project/mastering-fire/authentication/providers):
1. choose authentication
2. choose Sign-In-Methods
3. choose the methods of Sign in you need 
#### ⛏Activate Authentication via my Flutter Project:
1. download general package for authentication [`firebase_auth` | Flutter package](https://pub.dev/packages/firebase_auth)
2. download package for each authentication method
3. Import the plugin in your Dart code:
```dart
import 'package:firebase_auth/firebase_auth.dart';
```
___
### 📌Different Sign-in Methods:
- with email and password (requires creating account first)
- google 
- Facebook (requires MacBook for iOS authentication)
- Phone Number Authentication
- GitHub, Twitter
- Apple Sign-In
- Anonymous Authentication (allowing users to try the app **without creating an account**)
___
### 📌Tips and Tricks:

>[!NOTE] > Tracking Authentication State if the user is sign in or out during debug this method should be called in the main function

>[!TIP] > save your sign in method in the local storage so when you sign out, use only the suitable code according to the platform you used to sign in

>[!NOTE] > Use email verification when you try to sign in to ensure this account is real one (this is used in sign in with email and password method)

___
### 📌Social Authentication:
[Social Authentication | FlutterFire](https://firebase.flutter.dev/docs/auth/social)
#### ⛏Sign-In with Google Account:
1. download package: [google_sign_in | Flutter package](https://pub.dev/packages/google_sign_in)
2. go go google console and allow google authentication in sign-in methods
3. get **SHA-1** and **SHA-256** from flutter project
	- method 1:
```dart
cd android
./gradlew signingReport
```
	- method 2:
```dart
keytool -list -v -keystore C:\Users\fox\.android\debug.keystore -alias androiddebugkey
```
- then type the password which is: `android`
4. initialize **SHA-1** and **SHA-256** in the firebase project
    - Go to your [Firebase Console](https://console.firebase.google.com/).
    - Open your project → Project Settings → **General** → **Your Apps** (under "Your apps" section).
    - Select your Android app and click **Add Fingerprint**.
    - Paste the SHA-1 value(s) here.
    - Download the updated `google-services.json`.
    - Place it in your Flutter project at `android/app/google-services.json`.

```dart
flutter clean
flutter pub get
```
5. run your project again:
___
#### 📃Sign-in With Facebook Account: 
- **download Package:** [flutter-Facebook-auth](https://pub.dev/packages/flutter_facebook_auth)
- in the firebase project console apply Facebook to be a sign-in method.
- Full documentation:[intro | Flutter Facebook auth](https://facebook.meedu.app/docs/7.x.x/intro/)
>[!NOTE] >Facebook requires Native setup for each OS 
##### ⛏Requires configuration for Android: [Android configuration](https://facebook.meedu.app/docs/7.x.x/android)
1. select an app or create new Facebook app | [Android - Facebook Login](https://developers.facebook.com/docs/facebook-login/android/?locale=en)
2. Edit **Your Resources and Manifest** add this config in your android project]
	- Open your `/android/app/src/main/res/values/strings.xml` file, or create one if it doesn't exists.
	    
	- Add the following (replace `{your-app-id}` with your Facebook app Id) and with your client token:
Here one example of `strings.xml`:
```xml
<?xml version="1.0" encoding="utf-8"?>

<resources>
    <string name="facebook_app_id">1033361245343316</string>
    <string name="facebook_client_token">75663c9e589e2833739028a066fe2c86</string>
</resources>
```
#### 💉Get the Facebook App Id and Client Token:
from my Facebook Apps: [All Apps - Meta for Developers](https://developers.facebook.com/apps/?show_reminder=true)
- App Settings:
	- basic--> `app_id`
	- advanced--> `client_token`
3. add some app permissions for android and some Queries:
	- Open the `/android/app/src/main/AndroidManifest.xml` file.
	- Add the following uses-permission element before the application element
```xml
<uses-permission android:name="android.permission.INTERNET"/>
```

	- Add the following meta-data element, an activity for Facebook, and an activity and intent filter for Chrome Custom Tabs inside your application element
```xml
<meta-data android:name="com.facebook.sdk.ApplicationId" android:value="@string/facebook_app_id"/>
<meta-data android:name="com.facebook.sdk.ClientToken" android:value="@string/facebook_client_token"/>
```
- add some queries:
```xml
<queries>  
	<provider android:authorities="com.facebook.katana.provider.PlatformProvider" />  
</queries>
```
- Here one example of `AndroidManifest.xml`:
```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="app.meedu.flutter_facebook_auth_example">
    <uses-permission android:name="android.permission.INTERNET" />
    <queries>  
		<provider android:authorities="com.facebook.katana.provider.PlatformProvider" />  
	</queries>
    <application
       android:name="${applicationName}"
       android:icon="@mipmap/ic_launcher"
       android:label="facebook auth">

       <meta-data
           android:name="com.facebook.sdk.ApplicationId"
           android:value="@string/facebook_app_id" />
       <meta-data 
           android:name="com.facebook.sdk.ClientToken" 
           android:value="@string/facebook_client_token"/>

        <activity
           android:name=".MainActivity"
           android:configChanges="orientation|keyboardHidden|keyboard|screenSize|smallestScreenSize|locale|layoutDirection|fontScale|screenLayout|density|uiMode"
           android:hardwareAccelerated="true"
           android:launchMode="singleTop"
           android:theme="@style/LaunchTheme"
           android:exported="true"
           android:windowSoftInputMode="adjustResize">
           <meta-data
               android:name="io.flutter.embedding.android.NormalTheme"
               android:resource="@style/NormalTheme" />
           <meta-data
               android:name="io.flutter.embedding.android.SplashScreenDrawable"
               android:resource="@drawable/launch_background" />
           <intent-filter>
               <action android:name="android.intent.action.MAIN" />
               <category android:name="android.intent.category.LAUNCHER" />
           </intent-filter>
       </activity>
       <meta-data
           android:name="flutterEmbedding"
           android:value="2" />
    </application>
</manifest>
```
4. Associate Your Package Name and Default Class with Your App and save all edits you have done. | [Android - Facebook Login](https://developers.facebook.com/docs/facebook-login/android/?locale=en)
##### 💉Get Package Name (Application ID):
in the `build.gradle` file : ex: `com.example.smart_garage_final_project`
##### 💉Activity class Name:
Default Activity Class Name be like: `com.example.smart_garage_final_project.MainActivity`
5. Provide the Development and Release Key Hashes for Your App:
###### 💉How to get the Key Hashes:
- download OpenSSL and put initialize it in environment variables
- open `cmd`
- write the path of OpenSSL which is : `cd "C:\Program Files\OpenSSL-Win64\bin"`
- write the command to get the keys in this path:
```
keytool -exportcert -alias androiddebugkey -keystore "C:\Users\fox\.android\debug.keystore" -storepass android | "C:\Program Files\OpenSSL-Win64\bin\openssl.exe" sha1 -binary | "C:\Program Files\OpenSSL-Win64\bin\openssl.exe" base64
```
##### 💉Allow Facebook authentication in Firebase Project.
**in the firebase sign-in methods:**
from basic app secret:
- add the app id
- add the app secret
- and copy the link below them.
**in the Facebook application:**
from the use case:
- choose settings
- put the link you have copied in the `Valid OAuth Redirect URIs` section
- save the changes
___
##### Give Permissions to Email Testing:
**in the Facebook app Project Use cases:**
- go to permissions
- in the email press `add` to be converted to `ready for testing`
___
##### ⛏Requires configuration for iOS: [iOS configuration | Flutter Facebook Auth](https://facebook.meedu.app/docs/7.x.x/ios)

>[!error] >implementing Facebook authentication for an iOS app requires a Mac computer. This is because iOS app development generally needs `Xcode`, which is only available on macOS.

___
### 📌Snippet Code:
![[Firebase-authentication-consumer]]
___
### 📌Another Concepts need to Cover:
Besides sign-in methods, here are **important features** used in professional apps:
- **Linking Accounts**
    
    - Example: A user signs in with Google, then wants to also link their Facebook or email account.
        
    - Helps in account recovery or merging multiple login methods.
        
- **Re-authentication**
    
    - Required for **sensitive actions**, like changing email, password, or deleting an account.

- **Session Management**
    
    - Know how to detect expired sessions or tokens.
        
    - Use `FirebaseAuth.instance.authStateChanges()` to monitor sign-in status.
        
- **Security Rules (Firestore/Realtime DB)**
    
    - Customize access control based on authentication state and user roles.
        
- **Custom Claims / Roles**
    
    - Use for **admin users**, premium features, etc.
        
    - Set claims via Firebase Admin SDK (not directly from Flutter).
        
- **Multi-Factor Authentication (MFA)**
    
    - Firebase recently added this, but **only for some providers** like email or phone.
        
    - Adds a second layer of security.
        
- **Custom Authentication System**
    
    - You create your own backend and use Firebase's `signInWithCustomToken`.
        
    - Needed for enterprise or hybrid systems.
