## Resources:
[Bottom Sheet-Tutorial](https://youtu.be/XhWw_ad4ES8?si=NlE54MQycIadn9mO)
[showModalBottomSheet function-Documentation](https://api.flutter.dev/flutter/material/showModalBottomSheet.html)
[ BottomSheet في فلاتر - عرب فلاتر](https://arabflutter.com/bottomsheet-widget/#1-backgroundcolor)
___
## Fields:
- context: context
- `isDismissible`: bool  بتحدد اذا كانت قاللة للإختفاء أو لأ
- `backgroundColor`: Color
- shape: 
- builder: (context)=>Widget
___
## Code:
```dart
showModalBottomSheet(
	context: context,
	isDismissible: true,
	backgroundColor: Colors.amber,
	shape: RoundedRectangleBorder(
		borderRadius:
			BorderRadius.vertical(top: Radius.circular(30))),
	builder: (BuildContext context) {
	  return Container(
		 height: 200,
		padding: EdgeInsetsDirectional.all(15),
	  );
	});
```
>[!Note] this function requires context if it gives error wrap it with [[Builder]] widget

