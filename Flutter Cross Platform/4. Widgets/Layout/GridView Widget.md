> automatic Scrolled matrix of widgets

Fields:
- physics: Types of Scroll
- clip: Clip.none
- `gridDelegate:` 
	- `SliverGridDelegateWithFixedCrossAxisCount( )`
		- `crossAxisCount:` number of columns needed
		- `childAspectRatio`: ratio of  (width/height) =>once you get greater height becomes smaller  =>(recommended to use)
		- `mainAxisSpacing`: spaces between rows
		- `crossAxisSpacing`: spaces between columns
		- `mainAxisExtent:` the height of the single item  =>( not recommended to use )



>[!Note] > should be wrapped with definite height.



