### **استخدام `Builder` لو انت داخل `Scaffold` لكن خارج `MaterialApp`**

لو المشكلة بتحصل لأنك بتحاول تستدعي `showModalBottomSheet` في مكان مفيهوش `context` مربوط بـ `MaterialApp`، جرب تلفه بـ `Builder`:

```dart
Builder(
  builder: (context) {
    return ElevatedButton(
      onPressed: () {
        showModalBottomSheet(
          context: context,
          builder: (BuildContext context) {
            return Container(
              padding: EdgeInsets.all(16),
              child: Text('Bottom Sheet Content'),
            );
          },
        );
      },
      child: Text('Show Bottom Sheet'),
    );
  },
)
```