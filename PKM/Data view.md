```dataview
table type,parent
```
```dataview
list
```

```dataview
table type as T,parent as P
```
```dataview
TASK where !completed and urgent
```
```dataview
CALENDAR file.ctime
```
```dataview
list from #project or #task  where type= "permenant"
```
___
### Sorting:
```dataview
list from #project or #task  where type= "permenant" sort file.size desc
```

