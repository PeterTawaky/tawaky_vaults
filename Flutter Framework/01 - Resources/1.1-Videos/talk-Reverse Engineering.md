---
created_at: 2025-04-10 03:31
type: Literature Note
tags:
  - app-security
  - talk
source: https://www.youtube.com/watch?v=2dv2ws9nBjU
---
نسخ flutter اللي ممكن تصدرها:
- debug=>Development and testing
- profile=>Performance testing and profiling
- release=>Deploying the final app to users
### Reverse Engineering:
- reach for the code in the release mode and all algorithms and service used.
- reach API keys and Secret Keys.
- reach any private static data in your code.
- reach any assets in your app (be careful Reaching to assets is much easier than any thing else)
- cracking games or payment methods
### More Info:
- reverse Engineering in native is much easier than in flutter.
### Reverse Engineering types:
- Decompiled Code Analysis
	- reaching source code
- dynamic analysis
	- downloading app in edited environment has more prerogatives than normal user
- code injection (memory injection)
	- reaching runtime and changing behavior of the app.
	- like: hacking games and reaching memory.
- Inspecting Network Traffic & API Calls
	- reaching APIs used in the app.
	- request and data sent.
	- tokens
	- editing the response received in the app
### How to Protect my App from Reverse Engineering:
- data that is saved in shared prefference should be encrypted.
- use flutter secure storage for saving any senstive data.


