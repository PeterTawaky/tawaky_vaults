to get all versions run this command in `cmd`:
```
flutter doctor -v
```
![[java gradle version.png]]
- java version: 21.0.4
- dart version: 3.6.2
- `sdk` version: 3.27.4
- check the suitable versions: [Compatibility Matrix](https://docs.gradle.org/current/userguide/compatibility.html)
for java 21 the suitable version is :  8.5
- then go to `gradle-wrapper.properties` and change the number to: 8.5
- then go to `setting.gradle` go to plugins section and change the version like:
	- id "`com.android.application`" version "8.2.1" apply false
>[!Note] > there is packages that requires a java version of fixed number so when you download it, cause an error in versions

