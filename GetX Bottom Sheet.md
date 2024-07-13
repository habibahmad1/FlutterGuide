# GetX Bottom Sheet Flutter
```dart
import 'package:flutter/material.dart';
import 'package:get/get.dart';

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
    );
  }
}

class HomePage extends StatelessWidget {
  const HomePage({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        backgroundColor: Colors.pink[400],
        title: Text("Bottom Sheet GetX"),
        foregroundColor: Colors.white,
      ),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            // showModalBottomSheet(
            //   context: context,
            //   builder: (context) => Container(
            //     color: Colors.red,
            //     child: ListView(
            //       children: [
            //         ListTile(
            //           title: Text("Home"),
            //           leading: Icon(Icons.home),
            //         ),
            //         ListTile(
            //           title: Text("Download"),
            //           leading: Icon(Icons.download),
            //         ),
            //       ],
            //     ),
            //   ),
            // );

            Get.bottomSheet(Container(
              height: 300,
              color: Colors.red,
              child: ListView(
                children: [
                  ListTile(
                    leading: Icon(Icons.home),
                    title: Text("Home"),
                  ),
                  ListTile(
                    leading: Icon(Icons.download),
                    title: Text("Download"),
                  ),
                ],
              ),
            ));
          },
          child: Text("Open Bottom Sheet"),
        ),
      ),
    );
  }
}

```
