# Animated Container Flutter
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
        child: Obx(() => AnimatedContainer(
              duration: Duration(seconds: 2),
              width: controller.active.isFalse ? 200 : 300,
              height: controller.active.isFalse ? 200 : 360,
              decoration: BoxDecoration(
                borderRadius: controller.active.isFalse
                    ? BorderRadius.circular(20)
                    : BorderRadius.circular(0),
                color: controller.active.isFalse ? Colors.amber : Colors.purple,
              ),
            )),
      )),
    );
  }
}

```
