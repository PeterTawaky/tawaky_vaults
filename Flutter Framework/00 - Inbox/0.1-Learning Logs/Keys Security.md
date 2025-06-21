---
tags:
  - api
  - notion-api
  - fire-base
  - app-security
parent: "[[Application Programming Interface|API]]"
type: Permanent Note
deeper: 
against:
---
### Step by Step:
1. Package: [flutter-dotenv | Flutter package](https://pub.dev/packages/flutter_dotenv)
2. Create the file `.env` in your project
	- NOTION_API_KEY=KDFSLAJKLDSJF
	- NOTION_DATABASE_ID=DKSJFALDKFJA
3. Load our `.env` in main function
	- `await dotenv.load(fileName: '.env');`
4. In assets section of `pubspec.yaml` specify our `.env` file to be included in our application
	- `.env`
5. Include the file in `.gitignore`:
	- `*.env`
6. Now access anywhere in your code:
	-   `‘ ${dotenv.env[‘NOTION_DATABASE_ID’]}  ‘`
    

