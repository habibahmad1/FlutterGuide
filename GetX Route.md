# GetX Route Flutter
## Homepage Code
```dart
import 'package:flutter/material.dart';
import 'package:flutter_sample/pages/page1.dart';
import 'package:flutter_sample/pages/page2.dart';
import 'package:get/get.dart';

class HomePage extends StatelessWidget {
  const HomePage({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("GetX Route | Home"),
        backgroundColor: Colors.green,
        foregroundColor: Colors.white,
      ),
      body: ListView(
        padding: EdgeInsets.all(20),
        children: [
          ElevatedButton(
            onPressed: () {
              Navigator.of(context).push(MaterialPageRoute(
                builder: (x) => Page1(),
              ));
            },
            child: Text("Page-1"),
          ),
          ElevatedButton(
            onPressed: () {
              // Sama seperti push
              Get.to(Page2());

              // Sama seperti pushReplacement
              // Get.off(Page2());

              // Untuk ke home langsung tapi dia PushReplacement
              // Get.offAll(HomePage());

              // Untuk balik ke route sebelumnya
              // Get.Back();
            },
            child: Text("Page-2"),
          ),
        ],
      ),
    );
  }
}

```
