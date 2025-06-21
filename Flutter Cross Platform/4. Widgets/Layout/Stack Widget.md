> Used to Put Layers of Widget on each other

>[!Note] > the first Child is in the Bottom Layer of the stack

>[!Note] > by default the alignment is top left

>[!TIP] > Stack take the size of the largest child inside it, if any widget get out the stack frame it will be clipped.

>[!Important] > to control the alignment of a single child use: `Positioned Widget`
## Fields:
- children: []
- alignment: 
- `clipBehavior`:  `Clip.none`=>to stop the automatic clip when you get out from the stack frame
