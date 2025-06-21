## Why to use:
- can control it's color as an icon
- high quality
- used only for small icons
- not used for high details image
>[! Note] Convert PNG to SVG to Font

[SVG Converter - FreeConvert.com](https://www.freeconvert.com/svg-converter)
[Fontello - icon fonts generator](https://fontello.com/)

## Steps:
1. upload SVG image on the site `Fontello` (each image has `name` and `code`)
2. put the downloaded folder to assets folder
3. define this folder as a font in the `pubspec.yaml`
	1.  it's family name is the folder name
	2. it's path is `assets/icon/font/fontello.ttf`
4. create a class it's fields is `static` `constant` of type `IconData` and put family name and code for each font
5. use it in your app