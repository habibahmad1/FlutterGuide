# Dialog GetX Flutter
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
        title: Text("Snackbar GetX"),
        foregroundColor: Colors.white,
      ),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            // showDialog(
            //   context: context,
            //   builder: (context) => AlertDialog(
            //     title: Text("System"),
            //     content: Text("Ini pesan darurat"),
            //     actions: [
            //       TextButton(
            //           onPressed: () {
            //             Navigator.of(context).pop();
            //           },
            //           child: Text("Tutup"))
            //     ],
            //   ),
            // );

            Get.defaultDialog(
              title: "System",
              middleText: "Ini pesan darurat",
              textConfirm: "Cetak",
              textCancel: "Tutup",
              onConfirm: () => print("Ok"),
            );
          },
          child: Text("Open Dialog"),
        ),
      ),
    );
  }
}

```
