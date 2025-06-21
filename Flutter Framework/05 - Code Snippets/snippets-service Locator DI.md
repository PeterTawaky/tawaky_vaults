---
tags:
  - code-snippets
  - design-principles
parent: "[[Dependency Injection]]"
type: Permanent Note
deeper: 
against:
---
**Packages**: get-it
**file-name**: `di_container.dart`
```dart
final GetIt serviceLocator = GetIt.instance;

void setupDI() {
  serviceLocator.registerLazySingleton<DioConsumer>(() => DioConsumer());
  serviceLocator.registerLazySingleton<Dio>(() => Dio());
  serviceLocator.registerLazySingleton<NewsRepository>(() => NewsRepository());
}
```
==Better Way:== send `getIt` in this file and receive it in Constructor
```dart
void setupDI() {
  serviceLocator.registerLazySingleton<MyCubit>(() => MyCubit(serviceLocator()));
  serviceLocator.registerLazySingleton<MyRepository>(() => MyRepository(serviceLocator()));
  serviceLocator.registerLazySingleton<WebServices>(
      () => WebServices(WebServices.createAndSetupDio()));
}
```
___
Calling this function in the main function:
```dart
void main(){
setupDI();
}
```
___
How to access this instances:
```dart
DioConsumer dioConsumer = serviceLocator<DioConsumer>(); //dependency injection
```
