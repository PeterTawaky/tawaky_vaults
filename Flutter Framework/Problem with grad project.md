### Context with Cubit when change by `showModalBottomSheet`:
the problem is triggering function in the cubit but it's in different context cause i use builder widget as a parent i will provide you with the code:

### Problem Explanation

When you open a modal using `showModalBottomSheet`, the `context` inside that builder refers **only to the modal**, **not** to the context where your `BlocProvider` is available. That’s why `BlocProvider.of<ProfileCubit>(context)` may throw or not work as expected.
### Solution:
the solution simply is saving the context of cubit to use it again before entering the `ModalBottomSheet`
**the wrong code:**
```dart
Builder(
  builder: (context) {
    return GestureDetector(
      onTap: () {
        // Store the outer context before showing the bottom sheet
        final outerContext = context;
        showModalBottomSheet(
          context: context,
          builder: (context) {
            return Container(
              decoration: BoxDecoration(
                color: ColorsManager.white,
                borderRadius: BorderRadius.only(
                  topLeft: Radius.circular(20),
                  topRight: Radius.circular(20),
                ),
              ),
              height: 150.h,
              child: Column(
                children: [
                  Container(
                    width: width * 0.35,
                    height: 5.h,
                    margin: EdgeInsets.only(top: 10),
                    decoration: BoxDecoration(
                      color: ColorsManager.grey,
                      borderRadius: BorderRadius.circular(10),
                    ),
                  ),
                  ListTile(
                    title: Text('Camera'),
                    onTap: () {
                      // Use the outerContext to access the cubit
                      BlocProvider.of<ProfileCubit>(outerContext).uploadNewImage(
                        imageSource: ImageSource.camera,
                      );
                      Navigator.pop(context);
                    },
                  ),
                  ListTile(
                    title: Text('Gallery'),
                    onTap: () {
                      // Use the outerContext to access the cubit
                      BlocProvider.of<ProfileCubit>(outerContext).uploadNewImage(
                        imageSource: ImageSource.gallery,
                      );
                      Navigator.pop(context);
                    },
                  ),
                ],
              ),
            );
          },
        );
      },
      child: BlocBuilder<ProfileCubit, ProfileState>(
        buildWhen: (previous, current) =>
            current is SetRealImage || current is SetTempImage,
        builder: (context, state) {
          if (state is SetRealImage) {
            return ClipOval(
              child: Image.file(
                state.image,
                width: 70.w,
                height: 80.h,
                fit: BoxFit.cover,
              ),
            );
          } else if (state is SetTempImage) {
            return ClipOval(
              child: Image.asset(
                state.image,
                width: 70.w,
                height: 80.h,
                fit: BoxFit.cover,
              ),
            );
          }
          return SizedBox();
        },
      ),
    );
  },
),
```
**the right code:**
```dart
Builder(
  builder: (context) {
    return GestureDetector(
      onTap: () {
        final profileCubit = BlocProvider.of<ProfileCubit>(context); //saving the cubit context
        showModalBottomSheet(
          context: context,
          builder: (context) {
            return Container(
              // ... same container code
              child: Column(
                children: [
                  // ... other widgets
                  ListTile(
                    title: Text('Camera'),
                    onTap: () {
                      profileCubit.uploadNewImage(
                        imageSource: ImageSource.camera,
                      );
                      Navigator.pop(context);
                    },
                  ),
                  ListTile(
                    title: Text('Gallery'),
                    onTap: () {
                      profileCubit.uploadNewImage(
                        imageSource: ImageSource.gallery,
                      );
                      Navigator.pop(context);
                    },
                  ),
                ],
              ),
            );
          },
        );
      },
      // ... rest of the code
    );
  },
),
```
___
### Second one:
The issue you're facing is due to the fact that you're using a `Future.delayed` to update the elevator availability **after 10 seconds**, but the `ProfileCubit` is disposed immediately when the user navigates away from the page using `context.pushReplacement(AppRoutes.goParkScreen)`. As a result, the delayed callback is never executed, so the elevator remains unavailable.
============> Play in rules of database