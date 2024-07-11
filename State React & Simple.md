# State React & Simple
## ini Controllernya 
```dart
import 'package:get/get.dart';

class HomeControl extends GetxController {
  // Untuk Reactive State
  // var angka = 0.obs;

  // Untuk Simple State
  var angka = 0;

  void tambahData() {
    angka++;
    // update();
  }

  void updateState() {
    update();
  }
}

```

## Ini Kode Main
```dart
import 'package:flutter/material.dart';
import 'package:flutter_sample/controller/incrementC.dart';
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
      home: Homepage(),
    );
  }
}

class Homepage extends StatelessWidget {
  final homeC = Get.put(HomeControl());

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("State Management"),
        backgroundColor: Colors.transparent,
        foregroundColor: Colors.white,
        flexibleSpace: Container(
          decoration: BoxDecoration(
            gradient: LinearGradient(
                colors: [Colors.pink, Colors.orange],
                begin: Alignment.topLeft,
                end: Alignment.bottomRight),
          ),
        ),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            // Obx(() {
            //   return Text(
            //     "${homeC.angka}",
            //     style: TextStyle(fontSize: 48),
            //   );
            // }),

            GetBuilder<HomeControl>(
              builder: (controller) => Text(
                "${homeC.angka}",
                style: TextStyle(fontSize: 48),
              ),
            ),
            ElevatedButton(
              onPressed: () {
                homeC.tambahData();
              },
              child: Text("Tambah"),
              style: ElevatedButton.styleFrom(
                  backgroundColor: Colors.pink, foregroundColor: Colors.white),
            ),
            ElevatedButton(
              onPressed: () {
                // homeC.update();
                homeC.updateState();
              },
              child: Text("Update"),
              style: ElevatedButton.styleFrom(
                  backgroundColor: Colors.pink, foregroundColor: Colors.white),
            ),
          ],
        ),
      ),
    );
  }
}

```
