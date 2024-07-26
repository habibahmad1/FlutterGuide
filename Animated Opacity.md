# Animated Opacity Flutter
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
        child: Obx(() => AnimatedOpacity(
              duration: Duration(seconds: 2),
              opacity: controller.active.isFalse ? 0.1 : 1,
              child: Container(
                height: 150,
                width: 150,
                color: Colors.purple,
              ),
            )),
      )),
    );
  }
}

```
