# Animated CrossFade Flutter
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
        child: Obx(() => AnimatedCrossFade(
              firstChild: Container(
                width: 300,
                height: 300,
                color: Colors.orange,
              ),
              secondChild: Icon(
                Icons.handshake_rounded,
                color: Colors.pink,
                size: 300,
              ),
              crossFadeState: controller.active.isFalse
                  ? CrossFadeState.showFirst
                  : CrossFadeState.showSecond,
              duration: Duration(seconds: 3),
            )),
      )),
    );
  }
}

```
