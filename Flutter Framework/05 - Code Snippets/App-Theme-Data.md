---
tags: 
type: Unprocessed Note
aliases: 
against: 
parent: 
deeper:
---
```dart
class AppThemes {
  static final lightTheme = ThemeData(
      primaryColor: AppColors.primaryColor,
      scaffoldBackgroundColor: AppColors.whiteColor,
      fontFamily: AppFonts.mainFontName,
      textTheme: TextTheme(
        titleLarge: AppStyles.primaryHeadLinesStyle,
        titleMedium: AppStyles.subtitlesStyles,
      ),
      buttonTheme: ButtonThemeData(
        buttonColor: AppColors.primaryColor,
        disabledColor: AppColors.secondaryColor,
      ));
}
```