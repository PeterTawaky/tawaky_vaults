> the most important widget if flutter

### Some Uses of Container:
___
1. define any widget with fixed size
2. make background color for any widget
3. controlling the shape of some widgets like creating circle image by it
4. can apply gradient color in it
5. giving an outer frame to the card, image, button etc.. through giving it (color & padding) 
6. can give height to your text 
7. centering any widget inside it
8. `clipBehavior`: Clip.`antiAliasWithSaveLayer` =>to clip a stack and apply this changes
### some Fields:
___
- color:
- `borderRadius`: `BorderRadius`.circular()   => for making curves
- border: `Border`.all()   => for making edges
- width:
- height:
- alignment: وسطنة العناصر داخل الكونتينر
- padding: تباعدللعناصر الداخلية في الكونتينر بينما يظل هو محتفظا بحجمه
- margin: تباعد مسافة للكونتينر نفسه كاملا بكل ما فيه 
- child:
- `clipBehavior`: Clip.`antiAliasWithSaveLayer`
- decoration: [[BoxDecoration]]
- `boxShadow`: list of [[BoxShadow]]  ==>responsible  for making shadow to the item make it more real

### Limitations:
- you should give a known size to this widget through giving it width and height or even through wrap it with [[Expanded Widget]]
- if you put `BoxDecoration` widget you should remove the field `color` in the container and use it in the BoxDecoration only.