# State Reactive Flutter
## Controller
```dart
import 'package:get/get.dart';
import 'package:get/get_rx/get_rx.dart';
import 'package:get/get_rx/src/rx_types/rx_types.dart';

class HomeControl extends GetxController {
  RxInt angka = 0.obs;
  RxString data = "Belum ada data".obs;

  void tambah() => angka++;
  void kurang() => angka--;

  void dataUpdate() {
    data.value = "Sudah ada data";
  }

  void dataReset() {
    data.value = "Belum ada data";
  }
}

```

## Main Code
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
      body: ListView(
        padding: EdgeInsets.all(20),
        children: [
          Row(
            mainAxisAlignment: MainAxisAlignment.spaceBetween,
            children: [
              Obx(() => Text(
                    "${homeC.angka}",
                    style: TextStyle(
                      fontSize: 30,
                    ),
                  )),
              Row(
                children: [
                  ElevatedButton(
                    onPressed: () {
                      homeC.tambah();
                    },
                    child: Text("+"),
                    style:
                        ElevatedButton.styleFrom(backgroundColor: Colors.amber),
                  ),
                  SizedBox(width: 20),
                  ElevatedButton(
                    onPressed: () {
                      homeC.kurang();
                    },
                    child: Text("-"),
                    style:
                        ElevatedButton.styleFrom(backgroundColor: Colors.amber),
                  ),
                ],
              ),
            ],
          ),
          Row(
            mainAxisAlignment: MainAxisAlignment.spaceBetween,
            children: [
              Obx(() => Text(
                    "${homeC.data}",
                    style: TextStyle(
                      fontSize: 20,
                    ),
                  )),
              Row(
                children: [
                  ElevatedButton(
                    onPressed: () {
                      homeC.dataUpdate();
                    },
                    child: Text("Update"),
                    style:
                        ElevatedButton.styleFrom(backgroundColor: Colors.amber),
                  ),
                  SizedBox(width: 10),
                  ElevatedButton(
                    onPressed: () {
                      homeC.dataReset();
                    },
                    child: Text("Cancel"),
                    style:
                        ElevatedButton.styleFrom(backgroundColor: Colors.amber),
                  ),
                ],
              ),
            ],
          ),
        ],
      ),
    );
  }
}

```
