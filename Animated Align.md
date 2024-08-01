# Animated Align Flutter.
## Controller Code
```dart
import 'package:get/get.dart';

class HomeController extends GetxController {
  RxBool active = false.obs;
}

```

## Main Code
```dart
import 'package:flutter/material.dart';

import 'package:get/get.dart';

import '../controllers/home_controller.dart';

class HomeView extends GetView<HomeController> {
  const HomeView({Key? key}) : super(key: key);
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('HomeView'),
        centerTitle: true,
        backgroundColor: Colors.red,
        foregroundColor: Colors.white,
      ),
      body: Center(
          child: GestureDetector(
        onTap: () => controller.active.toggle(),
        child: Obx(() => Container(
              width: 300,
              height: 300,
              color: Colors.red,
              child: AnimatedAlign(
                duration: Duration(seconds: 2),
                alignment: controller.active.isFalse
                    ? Alignment.center
                    : Alignment.topRight,
                curve: Curves.fastOutSlowIn,
                child: Text(
                  "Animated",
                  style: TextStyle(fontSize: 22, color: Colors.white),
                ),
              ),
            )),
      )),
    );
  }
}

```
