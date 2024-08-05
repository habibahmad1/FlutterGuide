# CustomPainter Flutter
Untuk membuat desain custom
```dart
import 'dart:ui';

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
      ),
      body: Center(
        child: Container(
          width: 300,
          height: 300,
          color: Colors.grey[300],
          child: CustomPaint(
            painter: MyPaint(),
          ),
        ),
      ),
    );
  }
}

class MyPaint extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    Paint MyPaint = Paint()
      ..color = Colors.blue
      ..strokeWidth = 20
      ..strokeCap = StrokeCap.round;

    canvas.drawLine(
      Offset(0, 0),
      Offset(0, size.height),
      MyPaint,
    );

    canvas.drawLine(
      Offset(0, size.height),
      Offset(size.width / 2, size.height / 2),
      MyPaint,
    );

    canvas.drawLine(
      Offset(size.width / 2, size.height / 2),
      Offset(size.width, size.height),
      MyPaint,
    );

    canvas.drawLine(
      Offset(size.width, size.height),
      Offset(size.width, 0),
      MyPaint,
    );

    canvas.drawLine(
      Offset(size.width, 0),
      Offset(0, 0),
      MyPaint,
    );
  }

  @override
  bool shouldRepaint(covariant CustomPainter oldDelegate) {
    return false;
  }
}

```
