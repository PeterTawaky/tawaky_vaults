---
type: Fleeting Note
tags:
  - flutter-integrations
created_at: 2025-04-09 05:37
---
### في تلت طرق هوضحهملك في المقالة دي:
### ✅ **Option 1: Embed Google Form using WebView**

This is the **easiest way** if you're okay with showing the form as-is.

#### 🔧 Steps:

1. **Get the Google Form link:**
    
    - Open your form.
        
    - Click the “Send” button → Select the **link icon** → Copy the link.
        
2. **Add `webview_flutter` package:** In your `pubspec.yaml`:
```dart
dependencies:
  webview_flutter: ^4.2.2
```
3. **Use WebView in your widget:**
```dart
import 'package:flutter/material.dart';
import 'package:webview_flutter/webview_flutter.dart';

class GoogleFormPage extends StatelessWidget {
  final String formUrl = 'https://docs.google.com/forms/d/e/your_form_id/viewform';

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Fill the Form")),
      body: WebView(
        initialUrl: formUrl,
        javascriptMode: JavascriptMode.unrestricted,
      ),
    );
  }
}
```
### ✅ **Option 2: Open Google Form in Browser (External)**

If you prefer to just redirect the user to a browser.
```dart
import 'package:url_launcher/url_launcher.dart';

void openForm() async {
  final url = Uri.parse('https://docs.google.com/forms/d/e/your_form_id/viewform');
  if (await canLaunchUrl(url)) {
    await launchUrl(url, mode: LaunchMode.externalApplication);
  } else {
    throw 'Could not launch $url';
  }
}
```
### ✅ **Option 3: Submit Data to Google Form Programmatically**

If you want to **create a custom form UI** in Flutter and **submit the data to a Google Form**, you can do that too.

But it's a bit tricky:

- You need to find the **input field names (entry.xxxxxxx)** in the form.
    
- Then send a POST request to the form’s endpoint.
    

Let me know if you want to try that method — I can walk you through it step by step.