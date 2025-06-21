---
type: permanent
tags:
  - dart
parent: "[[Mastering Dart]]"
---
### 1. Why Error Happens?
- if there is any problem in internet connection during the process
- if there is any problem in the data coming from the internet
- the user insert wrong data

### 2. When to use Error Handling
1. when dealing with any __Background Thread__
2. when receiving data from any __API__
3. when Dealing with any __Local Data base__
### 3. Ways of Error Handling?
 ##### 1. try-catch Block:
	if the program crashed during any process catch block will be executed and the program will continue without stoping
	 
```dart
	 () async {
	  try {
	  //we need to create a variable to recive the future value
	  //block of code try to excecute
	  } catch (error) {
		//block of code in case of error
		print('$error')
		}
	},
```
##### 2. then-catchError
```dart
	(){
	  asyncFunctionName().then((value) {
	  /*
	  this code will be excecuted when the future 
	  function finish it's mission
	  */
	  //we don't need to create a variable as it return it's value as a prameter
	  //block of code try to excecute
	  }).catchError((Error) {
		//block of code in case of error
		print(Error.toString());
		});
	},
```
#### the difference between the two ways:
> [!TIP] > 1. That __then function__ will __never be executed__ until the asynchronous thread return it's value and totally finish it's mission 

> [!TIP] > 2. that __try and catch__ needs the keyword __await__ before calling the function and if it returns value create a variable to take this value

> [!NOTE] > just in case you want to throw an error by yourself for any reason you can use this function:
> ```dart 
throw('error message that will apear'); //it will excecute error then excecute the catch block 
#### Example on Code:
```dart
// Background Thread
Future<String> getName() async {

  return 'hello tawaky';

}

// try-catch block
() async {
	  try {
		String futureString = await getName();
		print(futureString);
		print('may be excuted before the background thread finishes');
	  } catch (error) {
		print('opps there was an error');
	  }
	},
// then-catchError
()  {
	getName().then((value) {
	print(value); 
	print('this will excute one by one');
	throw ('opps there was an error');
	  }).catchError((Error) {
            print(Error.toString());
	  });
	},
```

