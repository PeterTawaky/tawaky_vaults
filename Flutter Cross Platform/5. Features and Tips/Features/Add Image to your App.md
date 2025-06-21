- Download the Package: [image_picker](https://pub.dev/packages/image_picker)
- create a variable of type file that will contain the image later:
```dart
File? imgFile;  //the variable that will  carry the image in it
```
- show the image in your app if exist
```dart
 imgFile == null
	? SizedBox()
	: Expanded(child: Image.file(File(imgFile!.path))),
```
### Add Image from Your gallery:
- Create a function to open the gallery for you to choose your image after that you can trigger this function:
```dart

 getImage() async {
    final pickedImage =
        await ImagePicker().pickImage(source: ImageSource.gallery);
    if (pickedImage != null) {
      setState(() {
        imgFile = File(pickedImage.path);  //take the file of the path image
      });
      CachedData.setData(key: 'profilePhoto', value: pickedImage.path);  //the data will be cached is the path only
    }
  }
```
### Add Image from Camera:
- the only thing that will change is the type of the image source:
```dart
final pickedImage = await ImagePicker().pickImage(source: ImageSource.camera);
```
>[!Note] >- the image depends on the path of it that is stored on your mobile

>[!Note] > you can use shared preference to save this image locally on your phone.


