# SliverPersistentHeaderDelegate Flutter
Seperti APPBAR Sliver tapi bisa di custom.
```dart
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
            expandedHeight: 100,
            flexibleSpace: FlutterLogo(size: 300),
          ),
          SliverPersistentHeader(delegate: MyClass(), pinned: true),
          SliverList(
            delegate: SliverChildBuilderDelegate(
              (context, index) {
                return Container(
                  height: 100,
                  color: Colors.green,
                  child: Center(
                    child: Text("List-${index + 1}"),
                  ),
                );
              },
              childCount: 20,
            ),
          )
        ],
      ),
    );
  }
}

class MyClass extends SliverPersistentHeaderDelegate {
  @override
  Widget build(
      BuildContext context, double shrinkOffset, bool overlapsContent) {
    return Container(
      color: Colors.blue,
    );
  }

  @override
  // TODO: implement maxExtent
  double get maxExtent => 300;

  @override
  // TODO: implement minExtent
  double get minExtent => 50;

  @override
  bool shouldRebuild(covariant SliverPersistentHeaderDelegate oldDelegate) {
    return false;
  }
}

```
