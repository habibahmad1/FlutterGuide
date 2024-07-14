# GetX Binding Flutter
## Main Code
Disini tempat untuk inisialisasikan route sekaligus controller dengan binding, sehingga pada route page1 itu langsung gunakan Get.find.
```dart
import 'package:flutter/material.dart';
import 'package:flutter_sample/controller/counter.dart';
import 'package:flutter_sample/pages/homepage.dart';
import 'package:flutter_sample/pages/page1.dart';
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
      getPages: [
        GetPage(
          name: "/page1",
          page: () => Page1(),
          binding: BindingsBuilder.put(() => CounterController()),
        ),
      ],
    );
  }
}

```

## Page 1 Code
```dart
import 'package:flutter/material.dart';
import 'package:flutter_sample/controller/counter.dart';
import 'package:flutter_sample/pages/homepage.dart';
import 'package:flutter_sample/widget/button.dart';
import 'package:get/get.dart';

class Page1 extends StatelessWidget {
  CounterController counterC = Get.find();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Binding | Page 1"),
        backgroundColor: Colors.red[700],
        foregroundColor: Colors.white,
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Obx(() => Text(
                  "${counterC.data}",
                  style: TextStyle(fontSize: 28),
                )),
            Row(
              mainAxisAlignment: MainAxisAlignment.spaceEvenly,
              children: [
                CustomButton(
                  nameText: "-",
                  fungsi: () {
                    counterC.decrement();
                  },
                ),
                CustomButton(
                  nameText: "+",
                  fungsi: () {
                    counterC.increment();
                  },
                ),
              ],
            ),
            SizedBox(height: 30),
            CustomButton(
              nameText: "To Homepage",
              fungsi: () {
                Get.offAll(() => Homepage());
              },
            ),
          ],
        ),
      ),
    );
  }
}

```

# Class Binding
jadi jika memiliki banyak controller bisa gunakan bindings atau lebih mudah dikumpulkan pada class tersendiri jadi nanti tinggal panggil.
## Perubahan pada Main Code
```dart
getPages: [
        GetPage(
          name: "/page1",
          page: () => Page1(),
          binding: allBinding(),
        ),
      ],
```

## Pada file Class Binding
```dart
import 'package:flutter_sample/controller/counter.dart';
import 'package:get/get.dart';

class allBinding extends Bindings {
  @override
  void dependencies() {
    Get.lazyPut(() => CounterController());
    Get.lazyPut(() => CounterController());
  }
}

```
