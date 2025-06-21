> Searching happens among List

1. create an empty List that will Contains All data you will take from it later.
2. create an empty list to contain Filtered Data you will search for in future.
3. create a bool variable to know if searching or not and change UI according to this case.
4. build the body of the search which is text field.
5. process of adding data to filtered list according to the words that is changing in the text field.
6. build your UI According to the suitable List.
7. Handle if there is no data added yet
## Change App Bar Shape according to the bool variable:
>[!Note] >the `searchFieldController` must not be in the build function 
```dart
AppBar(
          title: isSearchOpened    
              ? TextField(                    //if user is searching
                  style: TextStyle(color: Colors.black),
                  controller: searchFieldController,
                  onChanged: (value) {  //send data to be filtered by any change
                    debugPrint(value);
                    filterData(input: value);    //a function to initiallize the filtered List
                  },
                  decoration: InputDecoration(
                      border: InputBorder.none, hintText: 'Search'),
                )
              : Text(               // if user is not searching
                  'Notes App',
                ),
          actions: [
            IconButton(
              onPressed: () {
                setState(() {
                  isSearchOpened = !isSearchOpened;      //cjamge the bool variable state
                  if (isSearchOpened == true) {      //the close icon function
                    setState(() {
                      filteredList.clear();
                      searchFieldController.clear();
                    });
                  }
                });
              },
              icon: Icon(
                isSearchOpened ? Icons.clear : Icons.search,
                color: Colors.white,
              ),
            ),
          ],
        ),
```
## Filtering among List of maps:
```dart
filterData({required String input}) {
//input is any change that happens in the text field
    setState(() {
      filteredList = allData                                 //allData is a List of Maps
          .where((element) => element['title']    //element is a map
              .toString()
              .toLowerCase()      //to ensure that  uper/lower case will not effect the operation
              .startsWith(input.toLowerCase()))     //compare with start        (you can use contains)
          .toList();
    });
  }
```

## Handling if no data added:
```dart
allData.isEmpty ? Widget Refers to that there is no data : ListView.builder() 
```
## Build UI according to suitable List:
```dart
ListView.builder(
// item count
	itemCount: filteredList.isEmpty
		? allData.length
		: filteredList.length,
	
	itemBuilder: (context, index) {
	  return Widget(
		filteredList.isEmpty
		  ? allData[index]['title']   //you are not searching
		  : filteredList[index]['title'],    //you are searching
	);


```