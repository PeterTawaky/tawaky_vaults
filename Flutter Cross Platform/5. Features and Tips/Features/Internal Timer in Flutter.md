> Concept of repeating function each period of time
> when this function repeated Change something 
## Function to Handle time different cases and Caching it:
```dart
 _startCount() {
    Timer.periodic(Duration(seconds: 1), (timer) { 
    //this function will be excecuted every 1 second
      setState(() {
        if (timeInSecond == 59) {
          timeInSecond = 0;  //reset seconds
          timeInMinutes++;
          CachedData.setData(
            key: KeysManager.timeInMinutes,
            value: timeInMinutes,
          );
        }
        if (timeInMinutes == 59) {
          timeInMinutes = 0;  //reset minutes
          timeInHours++;
          CachedData.setData(key: KeysManager.timeInHours, value: timeInHours);
        }
        CachedData.setData(
          key: KeysManager.timeInSeconds,
          value: timeInSecond++,
        );
      });
    });
  }
```
### How to stop the timer:
- inside this function make a condition that when it's done stop the timer
```dart
timer.cancel();
```
### Where to Start the timer (Call the function)?
- make it in the `initState`  =>work automatically when the screen opened.
- when press on a specific button.