# Sliver AppBar & Sliver List
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
            //pinned: true, //Selalu diatas app bar muncul
            floating: true, //Ketika scroll bawah ide ketika atas muncul dikit2
            snap:
                true, //Ketika scroll bawah ide ketika atas muncul banyak sesuai tinggi appbar dan floating harus true
            title: Text("AppBar Sliver"),
            backgroundColor: Colors.black,
            foregroundColor: Colors.white,
            actions: [
              IconButton(onPressed: () {}, icon: Icon(Icons.add)),
              IconButton(onPressed: () {}, icon: Icon(Icons.more_vert)),
            ],
            centerTitle: true,
            flexibleSpace: FlutterLogo(
              size: 100,
            ),
            expandedHeight: 200,
          ),
          SliverList(
            delegate: SliverChildBuilderDelegate(
              (context, index) {
                return Container(
                  height: 100,
                  child: Center(
                    child: Text(
                      "List ${index + 1}",
                      style:
                          TextStyle(fontSize: 22, fontWeight: FontWeight.bold),
                    ),
                  ),
                  color: myColors[index % myColors.length],
                );
              },
              childCount: 20,
            ),
          ),
        ],
      ),
    );
  }
}

```
