`SELECT` is a command used for getting data
for selecting id and email from user table
```sql
SELECT email , id from user
```
for selecting all columns and get all data from user table
```sql
SELECT * from `user`
```
get data with sorting Descending (Order)
```sql
SELECT * from `user` ORDER BY `age` DESC
```
Limit => بتحدد عدد الصفوف اللي هيرجعلي
```sql
SELECT * FROM `user` LIMIT 2
```
adding two Conditions together
```sql
SELECT * from `user` ORDER BY `age` DESC LIMIT 2
```
get all users of specific data
```sql
SELECT * FROM `user` WHERE age = 24
```
get user of ages more than a number:
```sql
SELECT * FROM `user` WHERE age > 24
```
And Operator
```sql
SELECT * FROM user WHERE age > 3 AND password = 'peter'
```
```sql
SELECT * FROM user WHERE age >20 AND age < 60
```
Or Operator
```sql
SELECT * FROM user WHERE age > 3 OR age = 3
```
Not Operator
```sql
SELECT * FROM user  WHERE NOT country='shoubra'
```
get Data without Repetition:
```sql
SELECT DISTINCT `country` FROM user
```
get maximum value :
```sql
SELECT MAX(age) FROM user
```
get minimum value:
```sql
SELECT MIN(age) FROM user
```
get Average value:
```sql
SELECT AVG(age) FROM user
```
get number of users:
```sql
SELECT COUNT(id) FROM user
```
get a non repeated count:
```sql
SELECT COUNT(DISTINCT country) FROM user;
```
getting the summation:
```sql
SELECT SUM(age) FROM user
```
Searching for data start with:
```sql
SELECT * FROM user WHERE `name` LIKE 'c%'
```
Searching for data end with:
```sql
SELECT * FROM user WHERE `country` LIKE '%a'
```
Searching for data contains:
```sql
SELECT * FROM user WHERE `country` LIKE '%a%'
```
Searching for data start, with and at least two characters:
```sql
SELECT * FROM user WHERE `country` LIKE 'c_%'
```
Searching for data start, with and at least three characters:
```sql
SELECT * FROM user WHERE `country` LIKE 'c__%'
```
Searching for data start and end with:
```sql
SELECT * FROM user WHERE `name` LIKE 'c%o'
```
 