# Carousel Slider Flutter
```dart
import 'package:flutter/material.dart';

import 'package:get/get.dart';

import '../controllers/home_controller.dart';

import 'package:carousel_slider/carousel_slider.dart';

class HomeView extends GetView<HomeController> {
  const HomeView({Key? key}) : super(key: key);
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('HomeView'),
        centerTitle: true,
      ),
      body: CarouselSlider(
        options: CarouselOptions(height: 200.0, autoPlay: false, padEnds: true),
        items: [1, 2, 3, 4, 5].map((i) {
          return Builder(
            builder: (BuildContext context) {
              return Container(
                width: MediaQuery.of(context).size.width,
                margin: EdgeInsets.symmetric(horizontal: 5.0),
                decoration: BoxDecoration(
                  color: Colors.amber,
                  borderRadius: BorderRadius.circular(10),
                  image: DecorationImage(
                      image: NetworkImage(
                        "https://picsum.photos/id/${120 + i}/300/300",
                      ),
                      fit: BoxFit.cover),
                ),
              );
            },
          );
        }).toList(),
      ),
    );
  }
}

```
