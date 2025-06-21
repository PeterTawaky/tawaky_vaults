---
tags:
  - inherited-widget
parent: 
type: Permanent Note
deeper: 
against:
---
### Use Case:
think that we can send a data from parent widget to a child widget but how can we send a data from child widget to a parent widget.
ex:
	lets say we have many text form fields and what we need is to send all this data through cubit trigger to the server
```dart
CustomForm( 
	//the data inside here
),
CustomForm(),
CustomForm(),
ElevatedButton(
	onPressed:(){
		//need here to trigger a function and send data to cubit
	}
)
```
we Have many Solutions to deal with that:
1. just create a global variable and use this variable in the both places and it will be seen in your all project.
2. create a specific object encapsulated contains all variable you need and you can pass it from here to anywhere you want
```dart
class FormInput{
	String? tffOne;
	String? tffTwo;
	String? tffThree;
}
```
```dart
FormInput formInput=FormInput(); //instance created

//they are only the same instance any change in them will be changed in the real one
CustomForm(formInput.tffOne),
CustomForm(formInput.tffTwo),
CustomForm(formInput.tffThree),
ElevatedButton(
	onPressed:(){
		//need here to trigger a function and send data to cubit
		send to cubit the: (formInput)
	}
)
```
3. ![[Provider as an Inherited Widget]]