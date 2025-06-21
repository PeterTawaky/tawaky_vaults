---
tags:
  - async-programming
parent: 
type: Permanent Note
deeper: 
against:
---
### Index:
- [[Future Data#Display Loading Indicator]]
- [[Future Data#Shimmer vs `Skeletonizer` Packages]]
- [[Future Data#Dealing With Future Image]]
- [[Future Data#Display Future Data on Screen]]
- [[Future Data#2. Using Future-Builder widget]]
___
### Display Loading Indicator:
1. `CircularProgressIndicator` Widget:
	widget that is most common used when trying to get a future data to give better UX that indicates there is a data coming here.
	- used one time in the screen can replace the whole screen or even just one component
2. Shimmer Package| [shimmer](https://pub.dev/packages/shimmer):
	modern style of indication loading which show grey container animated with white line movable in it.
	- used many times in the screen, for each component separately.
>[!TIP] always create `custom_shimer` Widget and change in the dimensions of container
```dart
shimmer.fromcolors(
baseColor: Colors.grey[300]
highLightColor: Colors.white
child: Container(
	width:
	height:
	color:Colors.grey[300]
	)
)
```
___
### Shimmer vs `Skeletonizer` Packages:
- **Shimmer** → ✅ **Better look and feel**, more modern and animated, but 🛠️ **uses more resources**.
    
- `**Skeletonizer**` → ✅ **Better performance**, lighter on the device, but 🎨 **less fancy visually**,more easier to use.
___
### Dealing With Future Image:
Package: [cached-network-image](https://pub.dev/packages/cached_network_image)

#### States Deals with:
get Data: view the image
error widget: another image or icon in case of there is nothing to show
place holder: put shimmer with image dimensions
### Code ex:
```dart

```
___
### Display Future Data on Screen:
	it's data that may take time to reach you and it may reach safely or some problems happen wile reciveing this data, so it needs [[Error Handling]]
#### where it comes from:
- from API
- from Database
- BaaS
#### Methods of Viewing Future Data on Screen:
1. making logic by yourself
2. using `FutureBuilder` widget
3. using Bloc State Management
#### 1.making Logic by my self be like: 
___
> the right place to ==trigger== this data is the widget you want this data to appear in , and here is the place to trigger data in the initial state before building the UI where the order is given to get this data from it's place and start building the UI without waiting the data let it come by time

> [!TIP] > initial state should be executed and can't wait any thing as it should happen before building the UI
```dart
void initState() {
    delayReciveData();
    super.initState();
  }
```
> this function is for (حنيكة) want to delay the triggering of Data
```dart
Future delayReciveData() {
    return Future.delayed(
        const Duration(
          seconds: 2,
        ), () {
      readData();
    });
  }
```
> here is the most important function where we ==get Data== in it that may take time to perform this take and after that it change the state of the application causing  app ==rebuild== to view this data in your UI

>[! NOTE] response is an empty list you create in the class to receive the data later in it, it should be non nullable variable
```dart
Future<void> readData() async {
    response = await sqlDb.readData("SELECT * FROM 'notes'");
    setState(() {
      isLoading = false;
    });
  }
```

#### example for the whole code:
```dart
class _HomeScreenState extends State<HomeScreen> {
  List<Map> response = [];  //container to receive the data in it
  bool isLoading = true; //it's default value is there is no data at the beggining
  //instance
  SqlDb sqlDb = SqlDb();
  //function to read the data from the database

  Future<void> readData() async {
    response = await sqlDb.readData("SELECT * FROM 'notes'");
    setState(() {
      isLoading = false;
    });
  }

  Future delayReciveData() {
    return Future.delayed(
        const Duration(
          seconds: 2,
        ), () {
      readData();
    });
  }

  @override
  void initState() {
    delayReciveData();
    super.initState();
  }
}
```

___
### 2. Using [[Future-Builder widget]]:
	the most simplest way that you will really use in your code and it will be           explained in a separated page.
>[!important] ### the main difference between the two ways is the place of trigger:

- in [[Future-Builder widget]] the trigger happens in the ==future== field
- but by logic trigger happens in the initial state
> Used to handle the future data in the UI and trigger the future function request

- can view loading data indicator until data reached
- can handle error by building error widget
- can view the future data
>[!TIP] >best practice to use with `StatefulWidget` to make the request in the `initState` and save it in a variable then use this variable in the future field inside `FutureBuilder( )`.

```dart
var futureData;

  @override
  void initState() {
    futureData = NewsService.getBreakingNews(q: 'recommend'); //trigger
    super.initState();
  }
  
```

```dart
FutureBuilder<List<BreakingNewsModel>>(
        future: futureData,
        builder: (context, snapshot) {
          if (snapshot.hasError) {
            return Text('Error: ${snapshot.error}');
          } else if (snapshot.hasData) {
            return ListView.separated(
              separatorBuilder: (context, index) => SizedBox(height: 10.h),
              physics: NeverScrollableScrollPhysics(),
              shrinkWrap: true,
              itemCount: snapshot.data?.length ?? 0,
              itemBuilder: (context, index) {
                return NewsTile(breakingNewsModel: snapshot.data![index]);
              },
            );
          } else {
            return CircularProgressIndicator();
          }
        },
      ),
```
>[!NOTE] >Future Builder is mostly used in the Widget of Building the List not with each Single item.

