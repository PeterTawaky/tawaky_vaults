	make the whole screen scrooled with one scroll, handling all listviews builder in it.

- all it's Slivers (Children) must be of type `Sliver` 
- if Fixed height Widget then use: `SliverToBoxAdapter()` 
- if list that has not fixed height (vertical-scrollable):
	- `SliverList`
	- `SliverGrid`
- you can make padding using `SliverPadding()`
### Code Example:

```dart

```