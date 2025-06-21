> Use Search Delegate (it send you to another screen)

1. trigger the built-in function `showSearch`:
```dart
onPressed: () {
	showSearch(context: context, delegate: MySearch());  //MySearch class extends from  SearchDelegate
},
```
2. create the `MySearch` Class:
	- `buildActions` for close button
	- `buildLeading` for back button
	- `buildResults` for result screen
	- `buildSuggestions`  build the suggestions according to search
___
```dart
import 'package:flutter/material.dart';
import 'package:searching_search_delegate/result_screen.dart';

class MySearch extends SearchDelegate {
  List<String> carBrands = [
    "Toyota",
    "Honda",
    "Ford",
    "Chevrolet",
    "Mercedes-Benz",
    "BMW",
    "Audi",
    "Volkswagen",
    "Porsche",
    "Lamborghini",
    "Ferrari",
    "Tesla",
    "Nissan",
    "Hyundai",
    "Kia",
    "Jeep",
    "Dodge",
    "Subaru",
    "Mazda",
    "Mitsubishi",
    "Lexus",
    "Cadillac",
    "Buick",
    "Volvo",
    "Land Rover",
    "Jaguar",
    "Peugeot",
    "Renault",
    "Alfa Romeo",
    "Fiat",
    "Chrysler",
    "Lincoln",
    "Acura",
    "Infiniti",
    "Genesis",
    "Bugatti",
    "Rolls-Royce",
    "Bentley",
    "McLaren",
    "Aston Martin"
  ];

  String? selectedBrand; // متغير لتخزين العنصر المختار

  @override
  List<Widget>? buildActions(BuildContext context) {
    return [
      IconButton(
        onPressed: () {
          query = ''; // مسح البحث
        },
        icon: Icon(Icons.close),
      )
    ];
  }

  @override
  Widget? buildLeading(BuildContext context) {
    return IconButton(
      onPressed: () {
        close(context, null);
      },
      icon: Icon(Icons.arrow_back_ios),
    );
  }

  @override
  Widget buildResults(BuildContext context) {
    return ResultScreen(
      chosedTitle: selectedBrand ?? 'No Selection', // تمرير القيمة المختارة
    );
  }

  @override
  Widget buildSuggestions(BuildContext context) {
    List<String> suggestions = query.isEmpty
        ? carBrands
        : carBrands
            .where((element) => element.toLowerCase().contains(query.toLowerCase()))
            .toList();

    return ListView.builder(
      itemCount: suggestions.length,
      itemBuilder: (context, index) {
        return GestureDetector(
          onTap: () {
            selectedBrand = suggestions[index]; // تخزين العنصر المختار
            showResults(context);
          },
          child: Card(
            color: Colors.teal,
            child: ListTile(
              title: Text(suggestions[index]),
            ),
          ),
        );
      },
    );
  }
}

```