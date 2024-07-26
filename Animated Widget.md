# Animated Widget Flutter
## Controller Code
```dart
import 'package:flutter/widgets.dart';
import 'package:get/get.dart';

class HomeController extends GetxController
    with GetSingleTickerProviderStateMixin {
  late AnimationController myAnimated =
      AnimationController(vsync: this, duration: Duration(seconds: 2))
        ..repeat();
}

```

## Main Code
```dart
import 'dart:math';

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
        child: BoxWidget(animC: controller.myAnimated),
      ),
    );
  }
}

class BoxWidget extends AnimatedWidget {
  BoxWidget({super.key, required this.animC}) : super(listenable: animC);

  AnimationController animC;

  get muter => listenable as Animation<double>;

  @override
  Widget build(BuildContext context) {
    return Transform.rotate(
      angle: muter.value * 0.5 * pi,
      child: Container(
        width: 200,
        height: 200,
        color: Colors.teal,
      ),
    );
  }
}

```
