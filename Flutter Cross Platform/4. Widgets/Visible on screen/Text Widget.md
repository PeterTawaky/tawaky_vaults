### main use:
	printing String on the screen
### fields:
- 'my string'
- style: [[TextStyle]]
- `maxLines`:
- overflow: `TextOverFlow`.ellipsis
- `textAlign`:
## how can Text reach it's fixed Text Style in the System:
`style: Theme.of(context).textTheme.headlineLarge,`
>[!TIP] you can change the style of the `headLineLarge` from the [[ThemeData]]

- you even can take the Theme and change some features in it like with keeping the other :
	- color
	- font
	- size
```dart
style: Theme.of(context).textTheme.headlineLarge!.copyWith( any change you want),
```
## create a different style for the same Text:
```dart
Text.rich(
	TextSpan(
	  children: [
		TextSpan(
		  text: 'I agree to ',
			  style: TextStyle(
				color: kLightWhite,
			  ),
		),
		TextSpan(
		  text: 'Privacy Policy',
		  style: TextStyle(
			decoration: TextDecoration.underline,
			decorationColor: kTextColor,
			color: kTextColor,
			fontFamily: kSpecialFont,
		  ),
		),
	  ],
	),
  )
```
>[! Note] > How to make the String totally appear whatever the dart sign inside the string: dollar sign , \n etc.. by using `rowString`
```dart
Text( r 'any other text or signs you want to write' ),
```
### Advanced Use:
```dart
Text(
	r'$'
	'${product.price}',
),
```