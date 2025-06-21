our package: [connectivity_plus | Flutter package](https://pub.dev/packages/connectivity_plus)

> عملية الاتصال بال internet هي عملية مستمرة طوال فترة التواجد بالصفحة ويمكن وضع حد لها (إيقافها) لتحسين الأداء عند ضمان عدم الحاجة لهذه الخاصية.

### Code for Bloc
```dart
import 'dart:async';
import 'package:bloc/bloc.dart';
import 'package:connectivity_plus/connectivity_plus.dart';
import 'package:meta/meta.dart';
part 'check_internet_event.dart';
part 'check_internet_state.dart';

class CheckInternetBloc extends Bloc<CheckInternetEvent, CheckInternetState> {
  late StreamSubscription<List<ConnectivityResult>> _subscription;
  CheckInternetBloc() : super(InternetInitialState()) {
    on<CheckInternetEvent>(
      (event, emit) {
        if (event is MobileDataConnectionEvent) {
          emit(InternetConnectionState(
              msg: 'Internet Connection with Mobile Data'));
        } else if (event is WifiConnectionEvent) {
          emit(InternetConnectionState(msg: 'Internet Connection with Wifi'));
        } else {
          emit(NoConnectionState(msg: 'check your internet Connection'));
        }
      },
    );
    //event will be added in the Bloc itself
    //no functions it put inside the bloc
    _subscription = Connectivity().onConnectivityChanged.listen(
      (List<ConnectivityResult> result) {
        if (result.contains(ConnectivityResult.mobile)) {
          add(MobileDataConnectionEvent());
        } else if (result.contains(ConnectivityResult.wifi)) {
          add(WifiConnectionEvent());
        } else {
          add(NoConnectionEvent());
        }
      },
    );
    
  }
  
 //for stoping this process
  @override
  Future<void> close() {
    _subscription.cancel();
    return super.close();
  }
}
```