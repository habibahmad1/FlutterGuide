# Animation Avatar Glow Flutter
```dart
import 'package:avatar_glow/avatar_glow.dart';
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
        child: AvatarGlow(
          glowColor: Colors.green,
          glowRadiusFactor: 0.3,
          glowCount: 3,
          child: ClipOval(
            child: Container(
                width: 150,
                height: 150,
                child: Image.network("https://picsum.photos/400/400")),
          ),
        ),
      ),
    );
  }
}

```
