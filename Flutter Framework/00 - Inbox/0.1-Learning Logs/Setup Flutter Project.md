---
tags: 
parent: 
type: Permanent Note
deeper: 
against:
---
### Index:
[[Setup Flutter Project#📌Create All Folders and Files Automatically Using Script]]
[[Setup Flutter Project#📌Folders Structure]]
[[Setup Flutter Project#📌Adding Images Automatically to the Project]]
[[Setup Flutter Project#📌Fixed Sizes for Responsive Apps]]
___

### 📌Create All Folders and Files Automatically Using Script:

To run this script:
1. Save this file as `tools/generate_structure.dart`
2. Make sure the `tool` directory exists at the root of your project
3. Run the script with: `dart tools/generate_structure.dart`
___
### 📌Folders Structure
#### Lib Folder:
##### 📁features/
- 📁splash/
- 📁onboarding/
- 📁authentication/
	- 📁sign-up
	- 📁sign-in
	- 📁`forget_password`
- 📁home/
	- 📁logic
	- 📁data
	- 📁presentation
		- 📁views
		- 📁widgets
- 📁profile/
- 📁cart/
- 📁search/
- 📁bazar/


>[!TIP] >all files in the core folder are shared between the whole app Features

___

### 📌Adding Images Automatically to the Project
- install extension in vs-code: assets gen
- don't forget to add the images folder to the `pubspec.yaml`
- add those Lines in the `pubspec.yaml`:
```yaml
flutter assets gen extension:
asset path: path bta3 elswr
output path: lib/core/utils/
file name: app_assets.dart
```
___
### 📌Fixed Sizes for Responsive Apps:
| Advantage                 | Explanation                                                            |
| ------------------------- | ---------------------------------------------------------------------- |
| 📱 **Responsive UI**      | Design elements based on percentages instead of fixed pixels.          |
| 🧮 **Scalable Logic**     | Easily reuse sizes across screen sizes: `blockWidth * 80` = 80% width. |
| 🎯 **Cleaner Code**       | No manual math everywhere: `context.blockWidth * 30` reads well.       |
| 🧩 **Consistent Spacing** | You can even use it for padding/margins uniformly.                     |
![[Size-Config]]
#### How to Use it:
```dart
Container(
  width: context.blockWidth * 80,
  height: context.blockHeight * 25,
)
```
```dart
Text(
  context.isMobile ? 'Mobile View' : 'Large Screen View',
);
```
