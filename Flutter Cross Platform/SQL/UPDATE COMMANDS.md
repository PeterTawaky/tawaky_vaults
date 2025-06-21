`UPDATE` used for override on data
change each 50 age to 22 age
```sql
UPDATE user SET age =22 WHERE age=50
```
```sql
UPDATE user SET `email` = 'tawaky@gmail.com' WHERE `password`='peter'
```
update more than one field
```sql
UPDATE user SET `email`='helloworkd', `password`='7amrfdsaa',`age`=37 WHERE `id`=1
```