---
tags:
  - responsive-adaptive
parent: "[[Responsive]]"
type: Permanent Note
deeper: 
against:
---
- for Sized Between Items Ex: `SizedBox( )`:
	- use `MediaQuery`
	
- for item sizes Ex:  in container
	- use `screen-util`
		- .h
		- .w
		- .r
		- .sp
___
## Best Practice for `MediaQuery`:
لما تستخدم `MediaQuery.of(context)`, كل ما يحصل تغيير في البيانات Flutter **بيعيد بناء (Rebuild) كل الواجهات اللي بتعتمد عليه!** ![😵‍💫](https://static.xx.fbcdn.net/images/emoji.php/v9/t18/1/16/1f635_200d_1f4ab.png) يعني لو بتستخدمه في أكتر من مكان ممكن يأثر على الأداء ويبطّأ التطبيق بدون داعي!
### Wrong Use:
```dart
final size = MediaQuery.of(context).size; 
final orientation = MediaQuery.of(context).orientation;
final textScaleFactor = MediaQuery.of(context).textScaleFactor;
```
### Right Use:
```dart
final size = MediaQuery.sizeOf(context);
final orientation = MediaQuery.orientationOf(context);
final textScaleFactor = MediaQuery.textScaleFactorOf(context);
```