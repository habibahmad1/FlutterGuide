# GetX Dependency Flutter
## Main Code
```dart
import 'package:flutter/material.dart';
import 'package:get/get.dart';
import './pages/firstPage.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return GetMaterialApp(
      debugShowCheckedModeBanner: false,
      home: FirstPage(),
    );
  }
}

```

## Controller Code
```dart
import 'package:get/get.dart';

class SatuController extends GetxController {
  Map<String, dynamic> data = {
    "name": "Rudi",
    "age": 23,
  };
}

```


## Pages 1 Code
```dart
import 'package:flutter/material.dart';
import '../Controller/homeControl.dart';
import 'package:get/get.dart';
import '../pages/secPage.dart';

class FirstPage extends StatelessWidget {
  final pageSatuC = Get.put(SatuController());

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Dependency"),
        backgroundColor: Colors.purple,
        foregroundColor: Colors.white,
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text(
              "Name : ${pageSatuC.data['name']}, ${pageSatuC.data['age']} Tahun",
              style: TextStyle(fontSize: 22),
            ),
            SizedBox(height: 30),
            ElevatedButton(
              onPressed: () {
                Navigator.push(
                    context,
                    MaterialPageRoute(
                      builder: (context) => SecPage(),
                    ));
              },
              child: Text("Next Page"),
              style: ElevatedButton.styleFrom(
                backgroundColor: Colors.purple,
                foregroundColor: Colors.white,
                shape: RoundedRectangleBorder(
                    borderRadius: BorderRadius.circular(7)),
              ),
            ),
          ],
        ),
      ),
    );
  }
}

```

## Page 2 Code
```dart
import 'package:flutter/material.dart';
import '../Controller/homeControl.dart';
import 'package:get/get.dart';

class SecPage extends StatelessWidget {
  SatuController pageDuaC = Get.find();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Page 2"),
        backgroundColor: Colors.purple,
        foregroundColor: Colors.white,
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text(
              "Page 2, Name : ${pageDuaC.data['name']}, ${pageDuaC.data['age']} Tahun",
              style: TextStyle(fontSize: 22),
            ),
            SizedBox(height: 30),
            ElevatedButton(
              onPressed: () {},
              child: Text("Next Page"),
              style: ElevatedButton.styleFrom(
                backgroundColor: Colors.purple,
                foregroundColor: Colors.white,
                shape: RoundedRectangleBorder(
                    borderRadius: BorderRadius.circular(7)),
              ),
            ),
          ],
        ),
      ),
    );
  }
}

```
