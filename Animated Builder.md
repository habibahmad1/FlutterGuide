# Animated Builder Flutter
## Controller Code
```dart
import 'package:flutter/widgets.dart';
import 'package:get/get.dart';

class HomeController extends GetxController
    with GetSingleTickerProviderStateMixin {
  late AnimationController myAnimated =
      AnimationController(vsync: this, duration: Duration(seconds: 5))
        ..repeat();
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
        child: Container(
          width: 300,
          height: 600,
          color: Colors.black,
          child: Stack(
            children: [
              AnimatedBuilder(
                  child: Container(
                    width: 50,
                    height: 50,
                    color: Colors.amber,
                  ),
                  animation: controller.myAnimated,
                  builder: (context, anim) {
                    return Positioned(
                      top: 0,
                      right: 2 *
                          (0.5 - (0.5 - controller.myAnimated.value).abs()) *
                          250,
                      child: anim!,
                    );
                  }),
            ],
          ),
        ),
      ),
    );
  }
}

```
