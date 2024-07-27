# Animated Decorated Box Transition Flutter
## Controller Code
```dart
import 'package:flutter/widgets.dart';
import 'package:get/get.dart';

class HomeController extends GetxController
    with GetSingleTickerProviderStateMixin {
  late AnimationController myAnimated =
      AnimationController(vsync: this, duration: Duration(seconds: 2))
        ..repeat(reverse: true);
}

```

## Main Code
```dart
import 'package:flutter/material.dart';

import 'package:get/get.dart';

import '../controllers/home_controller.dart';

class HomeView extends GetView<HomeController> {
  DecorationTween myDecor = DecorationTween(
    begin: BoxDecoration(
        color: Colors.red, borderRadius: BorderRadius.circular(60)),
    end: BoxDecoration(
      color: Colors.purple,
    ),
  );

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Home View'),
        centerTitle: true,
        backgroundColor: Colors.red,
        foregroundColor: Colors.white,
      ),
      body: Center(
        child: DecoratedBoxTransition(
          decoration: myDecor.animate(controller.myAnimated),
          child: Container(
            width: 300,
            height: 300,
          ),
        ),
      ),
    );
  }
}

```
