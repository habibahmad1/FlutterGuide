# Animation Lottie Flutter
```dart
import 'package:avatar_glow/avatar_glow.dart';
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';

import 'package:get/get.dart';

import '../controllers/home_controller.dart';

import 'package:lottie/lottie.dart';

class HomeView extends GetView<HomeController> {
  const HomeView({Key? key}) : super(key: key);
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Home'),
        centerTitle: true,
      ),
      body: Center(
        child: Container(
          width: 300,
          height: 300,
          child: Lottie.network(
              "https://lottie.host/2cd26d0e-13de-49e1-9b26-32920411cc43/v9HTiQEZQO.json"),
        ),
      ),
    );
  }
}

```
