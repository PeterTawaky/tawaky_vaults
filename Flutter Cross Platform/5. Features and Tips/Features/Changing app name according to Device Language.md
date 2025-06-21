- go to the path `android/app/src/main/res/values/styles.xml`
- in the `resources` tag: 
```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string name="app_name"> todo fire </string>
```
- create a folder `values-ar` and add the file `string.xml` to it and write:
```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string name="app_name"> تودو فاير </string>
</resources>
```
- go to the path `android/app/src/main/AndroidManifest.xml` in the `android:label` make the app name variable:
```xml
android:label="@string/app_name"
```
- run your app again