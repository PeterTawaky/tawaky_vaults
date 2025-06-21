---
tags:
  - UI-tricks
parent: 
type: Permanent Note
deeper: 
against:
---
### When to use Card:
	when you feel there is elevation shadow on the card floating on the screen, it's near to container

### Card Fields:
- elevation: use it to control the distance of the shadow from the card the most used value is: 10
- color: choose the color of the card you want
- child: padding Widget => Column Widget( )
### Best Practice:
	wrap this card with a container to control the card size and shadow colors,radius, direction
### Container Fields:
- width:
- height:
- `boxShadow`:  كل الأرقام اللي هنا بتتجرب لغية متوصل للشكل المظبوط
	- `blurRadius`: حدة الظل  good value=40
	- color: good color= grew with opacity( 0.2 )
	- `spreadRadius`:  انتشار الظل good value=0
	- offset: good value=  التحكم في اتجاه حركة الظل  Offset( 0 , 0 )
### How to put a photo on card like professional:
	you can put the photo on the card and make the image get out of your container to make more 3d shape by using Stack and Positioned widgets

```
Stack(
	children:[
		Card Layer Widget
		Positioned Widget=>Image Layer Widget
	]
)
```
>[!TIP] > if you used `GridView.builder` with the card remove the size of each single card (container) and use the ratios of width and height in the `GridView.builder` and wrap this grid with `Padding widget`

