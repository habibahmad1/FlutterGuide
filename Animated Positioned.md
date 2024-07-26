# Animated Positioned Flutter
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
          child: Container(
            width: 300,
            height: 600,
            color: Colors.black,
            child: Stack(
              children: [
                Obx(() => AnimatedPositioned(
                      duration: Duration(seconds: 2),
                      top: 0,
                      right: controller.active.isFalse ? 0 : 250,
                      child: Container(
                        width: 50,
                        height: 50,
                        color: Colors.amber,
                      ),
                    )),
              ],
            ),
          ),
        ),
      ),
    );
  }
}

```
