# Sliver AppBar & Sliver List
## Sliver AppBar
```dart
import 'package:flutter/material.dart';

import 'package:get/get.dart';

import '../controllers/home_controller.dart';

class HomeView extends GetView<HomeController> {
  const HomeView({Key? key}) : super(key: key);
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: CustomScrollView(
        slivers: [
          SliverAppBar(
            title: Text("AppBar Sliver"),
            backgroundColor: Colors.red,
            foregroundColor: Colors.white,
            actions: [
              IconButton(onPressed: () {}, icon: Icon(Icons.add)),
              IconButton(onPressed: () {}, icon: Icon(Icons.more_vert)),
            ],
            centerTitle: true,
            flexibleSpace: FlutterLogo(
              size: 100,
            ),
            expandedHeight: 100,
          ),
        ],
      ),
    );
  }
}

```
