# SliverGrid.count/extend Flutter
Untuk membuat grid tapi dalam bentuk sliver, Gunakan SliverGrid.count/extend agar lebih simple.
```dart
import 'dart:math';

import 'package:flutter/material.dart';

import 'package:get/get.dart';

import '../controllers/home_controller.dart';

class HomeView extends GetView<HomeController> {
  const HomeView({Key? key}) : super(key: key);
  @override
  Widget build(BuildContext context) {
    List<Color> myColors = [
      Colors.pink,
      Colors.amber,
      Colors.green,
      Colors.blue,
      Colors.purple,
    ];
    return Scaffold(
      body: CustomScrollView(
        slivers: [
          SliverAppBar(
            title: Text("SliverAppBar"),
            backgroundColor: Colors.red,
            foregroundColor: Colors.white,
            floating: true,
            expandedHeight: 20,
          ),
          SliverGrid.count(
            crossAxisCount: 3,
            children: List.generate(
              24,
              (index) {
                return Container(
                  color: Color.fromARGB(
                    255,
                    Random().nextInt(256),
                    Random().nextInt(256),
                    Random().nextInt(256),
                  ),
                );
              },
            ),
          )
        ],
      ),
    );
  }
}

```
