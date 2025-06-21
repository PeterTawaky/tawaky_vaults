## `Flutter Sdk`:
- Software Development Kit
- carries all prepared classes that you will use in your app
- the main Core of Flutter Platform Downloaded when you install Flutter
- to check the versions of `Flutter Sdk`: [versions](https://flutter-ko.dev/development/tools/sdk/releases)
- you can know your current `flutter sdk` version used through `cmd`:
```
flutter --version
```
- you can upgrade it through the `cmd`:
```
flutter upgrade
```
### How to Change `Sdk` Version in your project:
1. go to the path: `android/app/build.gradle`
2. change the `minSdkVersion` in the `defaultConfig`
![[minSdk Version.png]]
### How to Change the `Sdk` in your OS:
1. go to `Edit environment variables for your account`
2. choose `environment variables`
3. in the `user variable`: put the path of the `Sdk` version you want
#### Example Path:
`C:\src\flutter\bin`
___
## Gradle-Java compatibility:
- **Flutter Version**: The default Gradle version in new Flutter projects depends on the Flutter version you're using. If you want the latest defaults, consider updating Flutter to the latest stable version.
- Gradle version should be compatible with the java version
- you can check this through: [Compatibility Matrix](https://docs.gradle.org/current/userguide/compatibility.html)
- install the latest java version choose the` bin.msi`: [Java Downloads](https://www.oracle.com/java/technologies/downloads/)
- Now you should check your current Java version through `cmd`: 
```
java --version
```
- according to this java version install a suitable Gradle from: [Gradle | Releases](https://gradle.org/releases/?_gl=1*125bn9h*_gcl_au*MjEzNTA3NTc2MS4xNzM1MTM2ODQy*_ga*MjAzMTc0NzQyLjE3MzUxMzY4NDI.*_ga_7W7NC6YNPT*MTczNTEzNjg0Mi4xLjEuMTczNTEzNzIyNS40My4wLjA.)
- you can know the Gradle version installed on your OS through `cmd`:
```
gradle -v
```
>[!note]> the Gradle version installed Not necessarily to be the one that used in your project

![[compatibility.png]]
![[error.png]]
### How to Add Java and Gradle to the OS:
1. download java and setup it
2. go to system environment 
3. in the path of `system variables` & `user variable` put the `bin` folder of Java and Gradle
	- you can get the path of java from: `C:\Program Files\Java\jdk-23\bin`
	- you can get the path of Gradle from: `C:\gradle\gradle-8.10\bin`
4. create __GRADLE_HOME__ & __JAVA_HOME__ and put the path of the whole folders in it:
	- `C:\Program Files\Java`
	- `C:\gradle\gradle-8.10`
### Synchronize the `JDK` version in `cmd` according to the version you choose:
```
flutter config --jdk-dir="C:\Program Files\Java\jdk-20"
```
___
## Versions Used in your Project:
### Update Manually:
##### Get Gradle Version: 
you can change the `gradle` in the path `android/gradle/wrapper/gradle.wrapper.properties` with the new one
![[android gradle.png]]
### Update Automatically (best-way):
1. `open your project on the Android Studio`
2. but doesn't open the whole project choose to open the `Android Folder`
3. wait some time until scanning finishes
4. press Start (AGP) Upgrade in the bottom right of the screen
5. run selected steps
6. finally the Gradle in the path `android/gradle/wrapper/gradle.wrapper.properties` is updated
### but if it's not automatically updated:
1. press on file 
2. project structure
3. choose the Gradle version you want
___
## Update `Kotlin` Version in my Project if needed:

[Configure a Gradle project | Kotlin Documentation](https://kotlinlang.org/docs/gradle-configure-project.html)
![[Kotlin Version.png]]