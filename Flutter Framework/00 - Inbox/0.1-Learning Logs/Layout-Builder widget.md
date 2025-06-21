---
tags:
  - responsive-adaptive
parent: "[[Adaptive]]"
type: Permanent Note
deeper: 
against:
---
> it provides context-based screen constrains for widget building

> Widget used for making Adaptive UI design
- build different UI according to the screen width through the __constraints__

```dart
LayoutBuilder(builder: (context, constraints) {
          if (constraints.maxWidth > 1000) {
            //for windows
            return WindowsWidget();
          } else if (constraints.maxWidth > 600) {
            //for tablet
            return TabletWidget();
          } else {
            //for mobile
            return MobileWidget();
          }
        }),
```