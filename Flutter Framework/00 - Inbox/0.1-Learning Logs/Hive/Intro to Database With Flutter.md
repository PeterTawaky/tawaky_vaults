---
type: permanent
tags:
  - database
created_at: 2025-04-15 15:27
---
you aren't dealing directly with the data base but you deal with Database Management System.
![[person deal with database]]
### DBMS:
- Relational
- Non Relational
### Relational Database:
- How to know the data
	- save date in **tables** each row has **ID**
- How can I deal with it
	- through SQL (Structured Query Language)
- What I deal with:
	- oracle 
	- MySQL
	- SQLite
### Non Relational Database:
- How to know the data
	- key->value
- How can I deal with it
	- Language
	- API =>set of instructions (Ex: Hive-Shared Preferences)
- What I deal with:
	- MongoDB
	- Firebase
___
### Who Wins:
> كل جدول يكون متجمع تحت عنوان واحد:

- Tasks
- Person
- Products

|                 | SQL | NOSQL |
| --------------- | --- | ----- |
| القيود          | ✅   | ❌     |
| العلاقات        | ✅   | ❌     |
| مرونة الإستخدام | ✅   | ❌     |
| الأداء          | ❌   | ✅     |
___
### Plugins in Flutter:
- Hive-Non Relational(Fastest one)
- Shared Preference-Non Relational(fast)
- `SQFLite`-Relational(the Slowest)
