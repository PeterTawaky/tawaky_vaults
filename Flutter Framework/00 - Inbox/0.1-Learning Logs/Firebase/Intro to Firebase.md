---
tags:
  - BaaS
  - fire-base
parent: 
type: Permanent Note
deeper: 
against:
---
### Index:
- [[Intro to Firebase#📌Documentation]]
- [[Intro to Firebase#📌What Can Firebase do?]]
- [[Intro to Firebase#📌Setup Firebase in your Project]]
	- [[Intro to Firebase#📃For One Time]]
	- [[Intro to Firebase#📃For Each Project]]
___
### 📌Documentation:
[Flutter-Fire Overview](https://firebase.flutter.dev/docs/overview/)
[Firebase console](https://console.firebase.google.com/)
___
### 📌What Can Firebase do?
1. **Realtime Database**:
    - A NoSQL cloud database that stores and syncs data in real time.
    - Data is stored as JSON and synchronized across all connected clients in milliseconds.
    - Ideal for apps that require real-time updates, such as chat apps or live collaboration tools.
        
2. [[2.2. Cloud `Firestore`]]:
    - A more advanced NoSQL document-based database.
    - Offers better scalability, richer queries, and real-time synchronization.
    - Suitable for complex apps with structured data.
        
3. [[2.1]]:
    - Provides easy-to-use authentication methods, including email/password, phone authentication, and third-party providers like Google, Facebook, GitHub, and more.
    - Handles user management and secure authentication workflows.
        
4. **Cloud Storage**:
    - Offers secure and scalable file storage for user-generated content like images, videos, and audio.
    - Built on Google Cloud Storage, it integrates seamlessly with Firebase Authentication for secure access control.
        
5. **Hosting**:
    - Provides fast and secure static web hosting.
    - Supports custom domains, SSL certificates, and CDN (Content Delivery Network) for fast content delivery.
        
6. **Cloud Functions**:
    - Allows you to run server-side code in response to events triggered by Firebase features or HTTPS requests.
    - Written in Node.js, these functions are scalable and fully managed.
        
7. **Analytics**:
    - Provides detailed insights into user behavior and app performance.
    - Tracks user engagement, retention, and conversion rates.
        
8. **Crashlytics**:
    - A real-time crash reporting tool that helps identify and fix issues in your app.
    - Provides detailed crash reports, including stack traces and device information.
        
9. **Performance Monitoring**:
    - Monitors app performance, including startup time, network requests, and UI rendering.
    - Helps identify bottlenecks and optimize app performance.
        
10. **Test Lab**:
    - Allows you to test your app on real devices in the cloud.
    - Supports automated and manual testing.
        
11. **Push Notifications**:
    - Firebase Cloud Messaging (FCM) enables you to send notifications and messages to users across platforms (Android, iOS, web).
        
12. **Remote Config**:
    - Allows you to change the behavior and appearance of your app without requiring an update.
    - Useful for A/B testing and feature rollouts.
        
13. **Dynamic Links**:
    - Smart URLs that dynamically change behavior based on the platform and user context.
    - Useful for deep linking and sharing content.
        
14. **App Distribution**:
    - Simplifies the distribution of pre-release versions of your app to testers.
        
15. **Machine Learning (ML) Kit**:
    - Provides pre-built ML models for tasks like text recognition, image labeling, face detection, and barcode scanning.
    - Supports custom `TensorFlow` Lite models.
___

### 📌Setup Firebase in your Project:
#### 📃For One Time:
### Prepared Tools for one time: [CLI | Flutter-Fire](https://firebase.flutter.dev/docs/cli)
1. install (firebase CLI) on your windows [Firebase CLI reference  |  Firebase Documentation](https://firebase.google.com/docs/cli#setup_update_cli)
	1. open the app to ensure that you are logged in or not?
	2. if you are not logged in run the command:
	3. ensure authentication: صلاحية الكوماند لاين للتعامل مع الفاير بيز
```dart 
firebase login
```

```dart
firebase login --reauth
```
2. now open the `cmd` and run this  commands:
```
npm install -g firebase-tools
firebase --version
```
1. activate flutter fire command interface (FCI) in the command terminal: 
```
dart pub global activate flutterfire_cli
```
#### 📃For Each Project:
### Create Project on firebase : [FlutterFire Overview | FlutterFire](https://firebase.flutter.dev/docs/overview)
1. [Firebase console](https://console.firebase.google.com/?_gl=1*eoefil*_ga*OTkwMzMxMTU4LjE3MzAxMzA3MjU.*_ga_CW55HF8NVT*MTczNTkyOTQ2OS4xMi4xLjE3MzU5Mjk1OTUuMjguMC4w)
2. create project
3. add Project name
4. choose default account for Firebase
5. create project and wait
___
### How to add firebase to your Flutter project
6. install package in your pdoject: [firebase_core | Flutter package](https://pub.dev/packages/firebase_core)
7. create `firebase_option.dart` through command:
> this command fetch all project you done in fire base
```dart
flutterfire configure
```

8. choose project id and project name
9. choose the platform you need
10. write Bundle Id

>[! TIP] to make sure that all is done go to the project in console and you will be notified that your project is added

11. initialize firebase in your project for all files:
```dart
void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp(
    options: DefaultFirebaseOptions.currentPlatform,
  );
  runApp(MyApp());
}
```