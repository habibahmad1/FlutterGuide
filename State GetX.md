# State GetX Flutter
ini merupakan agar suatu Scaffold jika ada perubahan bisa hanya dengan Stateless, dan jika element ingin ada perubahan maka gunakan Obx() lalu bungkus element yang akandirender perubahan terus menerus di dalama itu.
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
      home: Homepage(),
    );
  }
}

class Homepage extends StatelessWidget {
  final myController = Get.put(Controller());

  @override
  Widget build(BuildContext context) {
    print("Render");
    return Scaffold(
      appBar: AppBar(
        title: Text("State Flutter"),
        backgroundColor: Colors.red,
        leading: Icon(Icons.account_circle_sharp),
        foregroundColor: Colors.white,
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Obx(
              () => Text(
                "${myController.data.value}",
                style: TextStyle(fontSize: 42),
              ),
            ),
            Row(
              mainAxisAlignment: MainAxisAlignment.spaceEvenly,
              children: [
                ElevatedButton(
                    onPressed: () {
                      myController.decrement();
                    },
                    style: ElevatedButton.styleFrom(
                        backgroundColor: Colors.red,
                        foregroundColor: Colors.white),
                    child: Text("-")),
                ElevatedButton(
                    onPressed: () {
                      myController.increment();
                    },
                    style: ElevatedButton.styleFrom(
                        backgroundColor: Colors.red,
                        foregroundColor: Colors.white),
                    child: Text("+")),
              ],
            )
          ],
        ),
      ),
    );
  }
}

class Controller extends GetxController {
  var data = 0.obs;
  increment() => data++;
  decrement() => data--;
}

```
