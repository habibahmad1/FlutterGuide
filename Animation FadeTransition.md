# Animation FadeTransition Flutter
## Controller Code
```dart
import 'package:flutter/material.dart';
import 'package:get/get.dart';

class HomeController extends GetxController
    with GetSingleTickerProviderStateMixin {
  late AnimationController animC = AnimationController(
    vsync: this,
    duration: Duration(seconds: 2),
  )..repeat(reverse: true);
}

```

## Main Code
```dart
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';

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
      ),
      body: Center(
        child: FadeTransition(
          opacity:
              CurvedAnimation(parent: controller.animC, curve: Curves.easeIn),
          child: Container(
            width: 300,
            height: 300,
            color: Colors.amber,
          ),
        ),
      ),
    );
  }
}

```
