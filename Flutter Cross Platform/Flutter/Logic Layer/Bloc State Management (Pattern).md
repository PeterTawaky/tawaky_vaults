





### Why this Logic:
1. __Events/functions__ : any interaction (trigger) in the application is an event that may cause an effect (State) in your app:
	- receive data from API
	- click on any button 
	- entering input
2. __States__ : each `thing` that change in your app is State , the reflection of the Event ,it's like using `setState` ,each state has a reflection change in your UI
	- initial state
	- no data
	- data loaded
	- change in any variable
	- theme
	- language
	- no internet
3. __bloc/cubit__ : take a streams of Events and push a streams of states, carry all variables and handle all logic in your app , the part who deals with the UI ,emit states to the UI to know which widget to build
![[bloc.png]]
### Use in Code:
 #### 1. Bloc
```dart
class CounterBloc extends Bloc<CounterEvent, CounterState> {
  int counter = 0;
  CounterBloc() : super(CounterInitialState()) {
    on<CounterEvent>((event, emit) {
    
      if (event is IncreamentEvent) {
        counter++;
        emit(CounterChangeValueState(counterValue: counter));
      } else if (event is DecreamentEvent) {
        counter--;
        emit(CounterChangeValueState(counterValue: counter));
      } else {
        counter = 0;
        emit(CounterChangeValueState(counterValue: counter));
      }
    });
  }
}
```
```dart
@immutable
sealed class CounterEvent {}  //abstract class
class IncreamentEvent extends CounterEvent {}
class DecreamentEvent extends CounterEvent {}
class ResetEvent extends CounterEvent {}
```
```dart
@immutable
sealed class CounterState {}
final class CounterInitialState extends CounterState {}
final class CounterChangeValueState extends CounterState {
  final int counterValue;
  CounterChangeValueState({required this.counterValue});
}
```
>[! NOTES] many events can cause the same state.

 #### 2. Cubit
 ```dart
 class GetCountCubit extends Cubit<CounterStates> {
  GetCountCubit() : super(InitialCounter());
  int counter = 0;
  //methods that will contain logic
  plusOne() {
    counter++;
    emit(Add()); //use Add state
  }
  minusOne() {
    counter--;
    emit(Subtract());
  }
}
```
```dart
abstract class CounterStates{}
class InitialCounter extends CounterStates{}
class Add extends CounterStates{
 final int counterValue;
  CounterChangeValueState({required this.counterValue});
}
class Subtract extends CounterStates{
 final int counterValue;
  CounterChangeValueState({required this.counterValue});
}
```
> as it shown `Cubit` seems more simple

>[! Tip] >the Variables in Bloc is the Changeable variables that will reflects in my UI so I need to pass this variable to my UI
>	pass it through the states fields

## How can we Work with this Files:
### 1. create bloc instance : 
>`only one instance` to use we create it lazy and bloc be available for all `Child Widgets` through `BlocProvider`

>[! NOTES] Should be the Parent Widget to all the children that uses the Bloc

>[!Note] you can use `BlocProvider` many times EX: before each screen to provide vs different instance in each screen

```dart
BlocProvider<YourBloc>(
        create: (context) => YourBloc(),
        child:const ChildWidget(),
      ),
```
### 2. make this lazy instance active:
> تفعيل ال_ Lazy Bloc_ داخل ال UI
> استدعاء اي function او event
```dart
//triger an event when click on button in Bloc
BlocProvider.of<YourBloc>(context).add(IncreamentEvent());
//or you can use:
context.read<YourBloc>.add(IncreamentEvent());
//triger an event when click on button in Cubit
??






```
> you can make it more easier if you will use it many times by defining a variable to access all bloc data and functions

```dart
CounterBloc bloc = BlocProvider.of<CounterBloc>(context)
 bloc.add(IncreamentEvent());
``` 
 
___
> making it more much Easier and static by creating this line in the Bloc it self in get function

```dart
// in the cubit file 
  static CounterCubit get(context) => BlocProvider.of<CounterCubit>(context);

//you can access this static function only by the name of this cubit in your code:
 CounterCubit cubit = CounterCubit.get(context);
```

### 3. Create Widgets will use this Bloc in App:
> توفير ال state وبناء ال widget
> used each time there is a change happens in UI
- `BlocBuilder` (most used)=> to return a widget
- `BlocListner` =>doesn't return widget used even in: `Navigate` , `Snackbar` , `dialog`
- `BlocConsumer` => collection of both of them
#### Apply on Code:
```dart

BlocBuilder<CounterBloc, CounterState>(
	  builder: (context, state) {
	  if(state is try the sate you want){
	  //how to reach the variable in this state====> state.variable
		  return Wiget
	  }else if(){
		  return Widget
	  }else{
		  SizedBox();
	  }
	  }
)
```
___
## Tricks and Advanced:
### Force App to Emit State:
```dart
BlocProvider<ToDoCubit>(
  create: (context) => ToDoCubit()..checkUncheckMark(),  //force to execute this function and emit the state inside it
  child: LoginScreen(),
);
```


## MultiBlocProvider to be Continue