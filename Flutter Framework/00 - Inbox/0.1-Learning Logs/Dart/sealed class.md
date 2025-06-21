---
type: permanent
tags:
  - dart
  - OOP
parent: "[[Mastering Dart]]"
---
## **متى تستخدم `sealed class`؟**

- عندما تحتاج إلى **ضمان التحكم في جميع الفئات المشتقة**.
- عند العمل مع **حالات معقدة** في **State Management**.
- عندما تريد **تحسين `switch` statement** والتأكد من تغطية جميع الحالات.
- إذا كنت بحاجة إلى **مرونة أكبر من `enum`**، مثل إضافة متغيرات خاصة لكل حالة.

---

## **الخلاصة**

- `sealed class` تمنع الوراثة خارج ملف المكتبة، مما **يعزز الأمان والتحكم**.
- تعمل بشكل مثالي مع **`switch` و `pattern matching`**، مما يساعد في **إدارة الحالات** بسهولة.
- تعتبر **أكثر مرونة من `enum`** لأنها تدعم **الوراثة وإضافة منطق إضافي**.
- مفيدة جدًا في **State Management** عند إنشاء حالات معقدة.
## Example of Sealed class uses:
### Handling Authentication:
```dart
sealed class AuthState {}

class Authenticated extends AuthState {
  final String userId;
  final String email;
  Authenticated(this.userId, this.email);
}

class UnAuthenticated extends AuthState {}

class AuthLoading extends AuthState {}

void handleAuthState(AuthState state) {
  switch (state) {
    case Authenticated(
      :String userId,
      :String email,
    ): //to get the value and use it or even you can access it through state.userId/state.email
      print('Authenticated with user:$userId and email:$email');
      break;
    case UnAuthenticated():
      print('UnAuthenticated');
      break;
    case AuthLoading():
      print('AuthLoading');
      break;
  }
}

void main() {
  AuthState currentState = AuthLoading();
  handleAuthState(currentState);
  
  currentState = Authenticated('123', '9TzQ7@example.com');
  handleAuthState(currentState);

  currentState = UnAuthenticated();
  handleAuthState(currentState);
}
```
### Handling Navigation:
```dart
sealed class NavigationEvent {}

class NavigationToHome extends NavigationEvent {}

class NavigationToProfile extends NavigationEvent {
  final String userId;
  NavigationToProfile(this.userId);
}

void handleNavigation(NavigationEvent event){
  if (event is  NavigationToHome){
    print('Navigating to Home');
  }else if (event is NavigationToProfile){
    print('Navigating to Profile for user ${event.userId}');
  }
}

void main() {
  handleNavigation(NavigationToHome());
  handleNavigation(NavigationToProfile('20200067'));
}
```
### Handling API Response using generic type:
```dart
sealed class ApiResponse<T> {} //using generic type with sealed class

class Success<T> extends ApiResponse<T> {
  final T data; //unknown data type
  Success(this.data);
}

class Failure<T> extends ApiResponse<T> {
  final String errorMsg;
  Failure(this.errorMsg);
}

class Loading<T> extends ApiResponse<T> {}

void handleApiResponse(ApiResponse response) {
  switch (response) {
    case Success():
      print(response.data);
      break;
    case Failure():
      print(response.errorMsg);
      break;
    case Loading():
      print('loading');
      break;
  }
}

void main() {
  ApiResponse<int> response = Loading();  //should initialize the generic type
  handleApiResponse(response);
  
  response = Success(200);
  handleApiResponse(response);
  
  response = Failure('Something went wrong');
  handleApiResponse(response);
}
```
