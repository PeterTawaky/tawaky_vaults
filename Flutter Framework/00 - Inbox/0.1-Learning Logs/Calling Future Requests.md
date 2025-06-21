---
tags:
  - api
parent: "[[Application Programming Interface|API]]"
type: Permanent Note
deeper: 
against:
---
### Sequential API calls:
	Each request waits for the previous one to complete. Useful if the second request **depends** on the first.
```dart
Future<void> fetchAllData() async {
  final user = await api.getUser();   // waits for this to finish
  final news = await api.getNews();   // then this starts
  return DashboardData(user: user, news: news);
}
```
### Parallel API calls:
	Both requests start immediately, and then you wait for both results. Much faster if the requests are **independent**.
```dart
Future<void> fetchAllData() async {
  final userFuture = api.getUser();   // starts immediately
  final newsFuture = api.getNews();   // starts immediately

  final user = await userFuture;
  final news = await newsFuture;

  return DashboardData(user: user, news: news);
}
```

### Tip for combining multiple Futures:
	You can also use `Future.wait()` if you have many requests:
```dart
Future<void> fetchAllData() async {
  final results = await Future.wait([
    api.getUser(),
    api.getNews(),
    api.getNotifications(),
  ]);

  final user = results[0] as User;
  final news = results[1] as List<NewsItem>;
  final notifications = results[2] as List<Notification>;

  return DashboardData(user: user, news: news, notifications: notifications);
}
```