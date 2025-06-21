> List of automatic Scrollable widgets can be viewed vertically or horizontally.

## `ListView`
>[!Note] > if you decided to view this list horizontally you must wrap the List view with a known Size: height ,width

>[!Note] > makes it's children take the whole width of the screen
### Fields:
- children:[ ]
- `scrollDirection`: `Axis.horizontal`
___
## `ListView.builder`
> automatic Looping to the List of Widgets

>[!Important] >the `Advantage` is the items is built one by one when you need it `Lazy Load`

>[!Note] >`ListView.builder` = `ListView` + `Loop`

### Fields:
- `itemCount`:
- `itemBuilder`: (context , index){ return widget }
- physics: 
- `shrinkWrap` : 
>[!Important] > `shrinkWrap` make the `listView` take the sized of all it's items one time but the disadvantage that the whole List is built one time that cause a load on the app

>[!Note] >through `Physics`you can `stop scroll` or `change the way of scrolling`
___
## `ListView.separated`
>used instead of `ListView.builder` when you need to make separation between each item

>[!Note] > `ListView.separated` = `ListView.builder` + `Seaparator Widget between each child`

### Fields:
- `itemCount`:
- `separatorBuilder` : (context , index){ return widget }
- `itemBuilder`: (context , index){ return widget }
- physics: 
>[!note] > Separator widget can be `Devider` or `Empty Space`

___
>[!Warning] >When you use a scrollable List inside another Scrollable List you will see problems here is some of the solutions can take:
1. Solution one: 
	- give the `ListView` a definite height by wrapping it with Sized box
2. Solution two:   ( Only used if the Whole Screen is not Scrollable  ( like: `Column` )
	- wrap the `ListView.builder` with Expanded Widget
3. Solution three:  ( Not the best Solution ):
	- force to stop the scroll in the second scrollable list by physics field and let the scroll done by the parent scrollable widget.
	- then make the `shrinkWrap` field `true` this make all the `ListView.builder` build all it's items in one time. which cause load on your app.
4. Solution four  ( Best One ):
	- [[CustomScrollView]]