---
tags:
  - design-principles
parent: "[[Dependency Injection]]"
type: Permanent Note
deeper: 
against:
---
first all this is provided by the package: [get-it](https://pub.dev/packages/get_it)
## 1.`registerSingleton<T>(instance)`

### 📌 What it does:
- only one instance for the whole app
### Use when:
- When you need to access the same instance **anytime, anywhere**.
- When it should be created **immediately** at app start.
### Best for: **Global services** that are always needed
**Examples:**
- `ThemeService`, `NavigationService`, `Logger`, `ConfigService`
### Best practice:
Register it in your `main()` function, before `runApp()`.
```dart
void setup() {
  getIt.registerSingleton<Logger>(Logger());
}
```
---
## 2.`registerLazySingleton<T>(() => T())`

### 📌 What it does:
- Creates the instance **only the first time it's needed**.
- Still a **singleton**, but **lazy-loaded**.
### Use when:
- You want to **save resources** (memory, CPU) at startup.   
- The service **may not always be used**.
### Best for: **Expensive or optional services**, created only when needed
**Examples:**
- `ApiService`, `DatabaseService`, `NotificationService`, `StorageService`
### Best practice:
Use this for services used later in the app (e.g., after login).
```dart
getIt.registerLazySingleton<ApiService>(() => ApiService());
```
---
## 3.`registerFactory<T>(() => T())`

### 📌 What it does:
- Creates a **new instance every time** you call `getIt<T>()`.
- This is the **Transient** lifetime.
### Use when:
- You want a **fresh instance every time**.
- The object holds **temporary UI state** or data per screen.
### Best for: **Stateless `ViewModels`, Controllers, Forms**
**Examples:**
- `LoginViewModel`, `ProfileFormViewModel`, `DialogController`
### Best practice:
Use this for short-lived objects tied to screens or dialogs.
```dart
getIt.registerFactory<LoginViewModel>(() => LoginViewModel());
```
## 4. `registerSingletonAsync<T>(Future<T> Function())`
### 📌 What it does:
- Registers a **singleton that needs `async` initialization**.
- Like when you want to `await` something like a DB or `SharedPreferences`.
### When to use:
- You need to `await` some setup before using the service.
- The service should be available **before the app runs**.
### Best for: **`Async`-initialized global services**
**Examples:**
- `SharedPreferences`, `FirebaseApp`, `Database` (SQLite)
### Best practice:
Use `await getIt.allReady()` before `runApp()` to ensure it's initialized.
```dart
void setup() async {
  getIt.registerSingletonAsync<SharedPreferences>(
      () async => await SharedPreferences.getInstance());

  await getIt.allReady(); // wait before launching the app
}
```
## 5.`registerLazySingletonAsync<T>(Future<T> Function())`

### 📌 What it does:
- Like `registerSingletonAsync`, but it **only initializes when first accessed**.
### When to use:
- You want the service to **load lazily and async**.
- You want to delay initialization **until first use**.
### Best for: `**Async`-initialized services** that may **not always be needed**
**Examples:**
- `CloudBackupService`, `RemoteConfigService`
