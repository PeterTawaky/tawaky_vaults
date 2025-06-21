---
tags:
  - notion-api
parent: 
type: Permanent Note
deeper: 
against:
---
### Index:
[[Notion-API#📌Documentations]]
[[Notion-API#📌Example Videos]]
[[Notion-API#📌Notion-API Requests]]
[[Notion-API#📌notion-API-Data Filtration]]
[[Notion-API#📌notion-API-Adding Properties to Database]]
___
### 📌Documentations:
[Build Notion API](https://developers.notion.com/)
[Notion API Requests](https://developers.notion.com/reference/intro)
___
### 📌Example Videos:
[Integrate API with Database](https://www.youtube.com/watch?v=7mo4XrjRFv0)
[Making your First Request](https://www.youtube.com/watch?v=3vhWx2LT-SY)
___
### 📌Notion-API Requests:
#### Required for all Notion-API Requests:
```dart
const String apiToken = 'YOUR_INTEGRATION_SECRET'; //notion api created from site
const String databaseId = 'YOUR_DATABASE_ID'; //notion database created in Notion
```
#### Required Headers for all Requests:
```dart
'Authorization': 'Bearer $apiToken',
'Notion-Version': '2022-06-28',
'Content-Type': 'application/json',
```
### Endpoints:
#### 📘 1. Databases:
==Query a Database (Retrieve Data)==
- **Endpoint:** POST /v1/databases/{`database_id`}/query
- **Purpose:** Fetch pages (rows) from a database, with optional filters, sorts, and pagination.
- **Example Use Case:** Display a list of tasks or __filter completed tasks__.
- can `sort data` according to any property.
```dart
const String url = 'https://api.notion.com/v1/databases/$databaseId/query';
  final response = await dio.post(
    url,
    options: Options(
      headers: {
        'Authorization': 'Bearer $apiToken',
        'Notion-Version': '2022-06-28',
        'Content-Type': 'application/json',
      },
    ),
    data: {
      // Optional: Add filters or sorts
      "filter": {"property": "Status", "select": {"equals": "Done"}},
      "sorts": [{"property": "$propertyName", "direction": "ascending"}],
    },
  );
```
==Retrieve a Database (Get Metadata)==
- **Endpoint:** GET /v1/databases/{`database_id`}
- **Purpose:** Fetch the database’s External structure, including its properties (e.g., column names and types-emoji-database id), title, and description.
- **Example Use Case:** Display the database title or dynamically build a UI based on its properties.
```dart
const String url = 'https://api.notion.com/v1/databases/$databaseId';
    final response = await dio.get(
      url,
      options: Options(
        headers: {
          'Authorization': 'Bearer $apiToken',
          'Notion-Version': '2022-06-28',
        },
      ),
    );
```
#### 📘 2. pages:
==Create a Page (Add a Row)==
- **Endpoint:** POST /v1/pages
- **Purpose:** Add a new page (row) to the database.
- **Example Use Case:** Let users add a new task from your Flutter app.
- you should add the properties according to the data base you sent to.
```dart
Future<void> createNotionPage(String title, String status) async {
const String url = 'https://api.notion.com/v1/pages';
    final response = await dio.post(
      url,
      options: Options(
        headers: {
          'Authorization': 'Bearer $apiToken',
          'Notion-Version': '2022-06-28',
          'Content-Type': 'application/json',
        },
      ),
	  data: {
		"parent": {"database_id": ApiKey.dataBasesId},
		"properties": {
		  "Phone": {  //property name
			"id": "%60D%5S%3A",  //property id
			"type": "phone_number",  //property type
			"phone_number": $phonevalue,  //property value
		  },
		  "Checkbox": {"id": "bjxi", "type": "checkbox", "checkbox": $checkvalue,},
		  "Number": {"id": "i%5ChS", "type": "number", "number": 2},
		  "Date": {
			"id": "q_%7Bj",
			"type": "date",
			"date": {"start": "2011-12-14", "end": null, "time_zone": null},
		  },
		  "Name": {  //title property
			"id": "title",
			"type": "title",
			"title": [  //property value
			  {
				"type": "text",
				"text": {"content": $titleName, "link": null},
				"annotations": {
				  "bold": false,
				  "italic": false,
				  "strikethrough": false,
				  "underline": false,
				  "code": false,
				  "color": "default",
				},
				"plain_text": $titleName,
				"href": null,
			  },
			],
		  },
		},
	  },
    );
```
==Retrieve a Page (Get a Single Row)==
- **Endpoint:** GET /v1/pages/{page_id}
- **Purpose:** Fetch details of a specific page (row) in the database.
- **Example Use Case:** Show detailed info when a user taps a list item.
```dart
  final String url = 'https://api.notion.com/v1/pages/$pageId';
    final response = await dio.get(
      url,
      options: Options(
        headers: {
          'Authorization': 'Bearer $apiToken',
          'Notion-Version': '2022-06-28',
        },
      ),
    );
```

___

### 📌notion-API-Data Filtration:
#### Filter by Created Time:
- The Notion API date format follows **ISO 8601**.
- first you should create the property Created time in your database.
```json
{
  "filter": {
    "property": "Created time",
    "date": {
      "on_or_after": "2025-03-27T00:00:00.000Z"  // 27/3/2025
    }
  }
}
```
#### 🛠 **More Filter Options**

You can modify the `filter` based on your needs:

- **Before a date:**
```json
"date": { "before": "2025-03-27T00:00:00.000Z" }
```
- **Exact match**:
```json
"date": { "equals": "2025-03-27" }
```
- **Between two dates:**
```json
"date": { "on_or_after": "2025-03-25", "on_or_before": "2025-03-27" }
```
#### 🙊Simple Issue:
the problem is that when enter the date like: 2025-03-28 it gives me data of the date after this which is : 2025-03-29.
#### Answer:
The issue you're encountering is likely due to **time zone differences** and how Notion interprets dates in its filters. When you pass a date like `"2025-03-28"`, Notion treats it as `"2025-03-28T00:00:00.000Z"` (midnight in UTC). If your pages are created in a different time zone (for example, a few hours ahead of UTC), their creation timestamp might actually fall on `"2025-03-28"` in your local time but on `"2025-03-29T..."` in UTC.
#### Deal With the Issue:
you request `28` notion response `29` 

___

### 📌notion-API-Adding Properties to Database:
> this process is done in the body of the request
#### 📃Select Property:
```json
{
  "properties": {
     "priority": {
        "select": {
          "options": [ // ← Must include options array
            {"name": "High", "color": "red"},
            {"name": "Normal", "color": "yellow"}
          ]
        }
      }
  }
}
```

#### 📃Check Property:
```json
{
    "properties": {
      "Done": {  // Name of the new checkbox property
        "checkbox": {}  // Property type definition
      }
    }    
}
```
#### 📃Text Property:
```json
{
  "properties": {
     "notes": {
        "rich_text": {} // ← Correct type name
      }
  }
}
```
#### 📃Date Property:
```json
{
  "properties": {
      "due_date": {
        "date": {}
      }
  }
}
```
#### 📃File Property:
```json
{
  "properties": {
      "attachments": {
        "files": {} // ← Plural "files" not "file"
      }
  }
}
```
#### 📃URL Property:
```json
{
  "properties": {
      "website": {
        "url": {}
      }
  }
}
```