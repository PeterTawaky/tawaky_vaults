### 1. Validation:
1. the parent widget of your screen should be `Form Widget` and put it's key field with variable
```dart
GlobalKey<FormState> validateKey = GlobalKey();

Form(
	key:validateKey
	child: ...
)
```
2. when trigger (on Pressed)
```dart
if(myKey.currenState.validate()){
	//go to your process
}else{
	//print not valid
}	
```
3. validator field in text form field 
```dart
TextFormField(
	validator: (val){
	//all you conditions
		if(val.isEmpty{
			return 'field can't be empty';
		}
	}
)
```
>[!Warning] > in any `Stateful` Widget dispose the `TextEditingController` you have created
```dart
@override
  void dispose() {
    categoryController.dispose();
    super.dispose();
  }
```
### 2. Design
>[!Note] the secret of `textfileld` design is in __`Border`__ 
#### Fields:
- controller: `TextEditingController()` => should be a variable
- enabled: true/false  هل المستخدم يقدر يدخله بيانات ولا لأ
- style: `TextStyle`(color: `Colors.black`, `fontSize`: 18),   //لتغيير لون النص الذي يكتبه المستخدم.
- decoration : 
	- `InputDecoration()`
		- `contentPadding` :    changing the size of text field
			- `EdgeInsets`.symmetric() 
				- vertical:
				- horizontal:
		- border:` OutlineInputBorder()`
			- `borderSide`:`BorderSide()`
				- color
			- `borderRadius` : `BorderRadius`.circular(x) 
		- `enabledBorder` :` OutlineInputBorder()`      (shape of border without clicking on it)
		- `focusedBorder` :` OutlineInputBorder()`      (shape of borer when the user is using it)

___
### How to clear the `textfield`:
```dart
//controller is the variable that refers to TextEditingController
controller.clear();
```