# GetX Route Flutter
## Homepage Code
```dart
import 'package:flutter/material.dart';
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
              // Navigator.of(context).push(MaterialPageRoute(
              //   builder: (x) => Page1(),
              // ));

              Navigator.of(context).pushNamed("page_1");
            },
            child: Text("Page-1"),
          ),
          ElevatedButton(
            onPressed: () {
              // Sama seperti push
              // Get.to(Page2());

              // Sama seperti pushReplacement
              // Get.off(Page2());

              // Untuk ke home langsung tapi dia PushReplacement
              // Get.offAll(HomePage());
              // Get.offAllNamed(HomePage());

              // Untuk balik ke route sebelumnya
              // Get.Back();

              // Untuk ke route yang sudah didaftarkan di Main Code pada getPage
              Get.toNamed("/page_2");
            },
            child: Text("Page-2"),
          ),
        ],
      ),
    );
  }
}
```

## Main Code
```dart
import 'package:flutter/material.dart';
import 'package:flutter_sample/pages/page1.dart';
import 'package:flutter_sample/pages/page2.dart';
import 'package:flutter_sample/pages/page3.dart';
import 'package:flutter_sample/pages/page4.dart';
import 'package:flutter_sample/pages/page5.dart';
import 'package:get/get.dart';
import './pages/home.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return GetMaterialApp(
      debugShowCheckedModeBanner: false,
      home: HomePage(),
      // routes: {
      //   "page_1": (context) => Page1(),
      //   "page_2": (context) => Page2(),
      //   "page_3": (context) => Page3(),
      //   "page_4": (context) => Page4(),
      //   "page_5": (context) => Page5(),
      // },

      getPages: [
        GetPage(name: "/homepage", page: () => HomePage()),
        GetPage(name: "/page_1", page: () => Page1()),
        GetPage(name: "/page_2", page: () => Page2()),
        GetPage(name: "/page_3", page: () => Page3()),
        GetPage(name: "/page_4", page: () => Page4()),
        GetPage(name: "/page_5", page: () => Page5()),
      ],
    );
  }
}

```
