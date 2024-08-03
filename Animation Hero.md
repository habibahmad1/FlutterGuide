# Animation Hero Flutter

## Home Code
```dart
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';

import 'package:get/get.dart';
import 'package:tutorial/app/routes/app_pages.dart';

import '../controllers/home_controller.dart';

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
        child: GestureDetector(
          onTap: () => Get.toNamed(Routes.PROFILE),
          child: Hero(
            tag: "anim",
            child: ClipOval(
              child: Container(
                width: 100,
                height: 100,
                child: Image.network("https://picsum.photos/500/500"),
              ),
            ),
          ),
        ),
      ),
    );
  }
}

```

## Profile Page
```dart
import 'package:flutter/material.dart';

import 'package:get/get.dart';

import '../controllers/profile_controller.dart';

class ProfileView extends GetView<ProfileController> {
  const ProfileView({Key? key}) : super(key: key);
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('ProfileView'),
        centerTitle: true,
      ),
      body: Center(
        child: Hero(
          tag: "anim",
          child: ClipOval(
            child: Container(
              width: 300,
              height: 300,
              child: Image.network("https://picsum.photos/500/500"),
            ),
          ),
        ),
      ),
    );
  }
}

```
