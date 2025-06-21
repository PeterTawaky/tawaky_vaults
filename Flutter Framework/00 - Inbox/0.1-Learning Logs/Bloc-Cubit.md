---
tags:
  - state-management
type: permanent
connections:
  - "[[bloc-Cubit Deals with UI]]"
  - "[[Cubit Provider-Builder can't be at same context]]"
aliases:
---
### Index:
- [[Bloc-Cubit#📌Intro to Bloc]]
- [[Bloc-Cubit#📌bloc-cubit Provide one instance]]
- [[Bloc-Cubit#📌bloc-Cubit Deals with UI]]
- [[Bloc-Cubit#📌Cubit Provider-Builder can't be at same context]]
- [[Bloc-Cubit#📌Trigger Bloc Functions]]
___
### 📌Intro to Bloc:
	Bussiness Logic Component, design pattern created by google. helps to separate between business logic layer and presentation layer, best state management solution.
#### Advantages:
- Separates UI and Logic
- Tracking the State Permanently
#### Bloc vs Cubit:
> bloc and cubit are the same idea with small difference.
1. Bloc: used in the big projects avoid overkilling by using it in small projects
2. Cubit: used in small and intermediate projects
![[Bloc Vs Cubit.jpg]]
___
### 📌bloc-cubit Provide one instance:
1. **`BlocProvider`**:
used to provide one instance of cubit to use it. maybe used for each screen or each widget you want, it create lazy instance until it's used later
```dart
BlocProvider<NewsCubit>(  //choose the cubit you will provide instance from it
  create:
	  (context) => NewsCubit()
  child: NewsTileList(),  //other child widget now can use this instance
),
```
___
2. **`RepositoryProvider`**:
used to provide one instance of repository to inject it to the cubit as a way of dependency management.
but it's better for me to use service locator dependency injection.
___
3. **`MultiBlocProvider`**:
provides many instances
___
### 📌bloc-Cubit Deals with UI:
 1. **`BlocBuilder`**:
rebuild the UI again with the new data update according to state

##### Where to put it:
Parent of the smallest widget that will change, even it's only a text widget
```dart
BlocBuilder<NewsCubit, NewsState>(  //cubit and states
      bloc: BlocProvider.of<NewsCubit>(context),   //the cubit you will use
      buildWhen: (previousState, currentState) => previousState != currentState,  //only cases that will rebuild
      builder: (context, state) {  //retuen widget that will be rebuild
        if (state is NewsLoaded) {
          return...
        } else if (state is NewsError) {
          return...
        } else {
          retur... 
        }
      },
    );
```

2. **`BlockListener`**:
do something when emit state, doesn't rebuild any widget:
- snack bar
- dialog
- navigate
- view something is hidden

##### Where to put it:
anywhere it doesn't effect on performance, as it doesn't rebuild any widget

same syntax as `BlocBuilder`

### Advanced Use:
check happening specific function as the same state can do different functions
create a Boolean variable in the state
```dart
if(state.hasIncremented){
//do something
}else if(state.hasDecremented){
//do something
}
```
3. **`BlockConsumer`**:
provides you both: `BlocBuilder` + `BlocListener`
4. **`MultiBlocBuilder`**:
5. **`MultiBlocListener`**:
provides many instances 
___
### 📌Cubit Provider-Builder can't be at same context:
#### Define the problem:
	the BlocProvider and BlocBuilder have the same context. so blocBuilder doesn't see the bloc provider in the context it needs new context to put it in so it can be seen.
```dart
build(BuildContext context) {
    return BlocProvider(
      create: (context) => NewsCubit(),
      child: BlocBuilder<NewsCubit, NewsState>(
        builder: (context, state) {}
      ),
    );
  }
```
#### The Solution:
	Builder Widget => it provides me with new context.so make it a parent widget to the bloc builder
```dart
build(BuildContext context) {
    return BlocProvider(
      create: (context) => NewsCubit(),
      child: Builder(
	      builder:(context)=>
		      BlocBuilder<NewsCubit, NewsState>(
		        builder: (context, state) {}
		      ),
      )
    );
  }
```
___
### 📌Trigger Bloc Functions:
1. Trigger through Bloc-Provider(when create instance):
used when you don't need to do an action to call a function in cubit, it's called by default, like in fetching data from API.
```dart
BlocProvider<NewsCubit>(
  create:
	  (context) => NewsCubit()..getNews(), //call function getNews by deafult
  child: NewsTileList(),
)
```
___
2. Trigger on Action:
```dart
BlocProvider.of<CounterCubit>(context).IncrementCounter()  //trigger the function in cubit
```
___
