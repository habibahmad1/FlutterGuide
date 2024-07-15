# GetX Storage Flutter
## Main Code
```dart
import 'package:flutter/material.dart';
import 'package:flutter_sample/pages/home.dart';
import 'package:flutter_sample/pages/login.dart';
import 'package:get/get.dart';
import 'package:get_storage/get_storage.dart';

void main() async {
  await GetStorage.init();
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return GetMaterialApp(
      debugShowCheckedModeBanner: false,
      home: LoginPage(),
      getPages: [
        GetPage(name: "/home", page: () => Home()),
        GetPage(name: "/login", page: () => LoginPage()),
      ],
    );
  }
}

```

## Login Page Code
```dart
import 'package:flutter/material.dart';
import 'package:flutter_sample/controller/login_controller.dart';
import 'package:get/get.dart';
import 'package:get_storage/get_storage.dart';

class LoginPage extends StatelessWidget {
  final box = GetStorage();
  final LoginController loginC = Get.put(LoginController());

  @override
  Widget build(BuildContext context) {
    if (box.read("rememberStorage") != null) {
      loginC.emailC.text = box.read("rememberStorage")['email'];
      loginC.passC.text = box.read("rememberStorage")['password'];
    }
    return Scaffold(
      appBar: AppBar(
        title: Text("Login Page"),
        backgroundColor: Colors.red[900],
        foregroundColor: Colors.white,
      ),
      body: ListView(
        padding: EdgeInsets.all(20),
        children: [
          TextField(
            controller: loginC.emailC,
            decoration: InputDecoration(
              labelText: "Email",
              border: OutlineInputBorder(),
            ),
            keyboardType: TextInputType.emailAddress,
            textInputAction: TextInputAction.next,
          ),
          SizedBox(height: 30),
          Obx(
            () => TextField(
              controller: loginC.passC,
              obscureText: loginC.isHidden.value,
              decoration: InputDecoration(
                suffixIcon: IconButton(
                  onPressed: () => loginC.isHidden.toggle(),
                  icon: Icon(Icons.remove_red_eye),
                ),
                labelText: "Password",
                border: OutlineInputBorder(),
              ),
            ),
          ),
          Obx(
            () => CheckboxListTile(
              contentPadding: EdgeInsets.symmetric(vertical: 0),
              value: loginC.remember.value,
              onChanged: (value) {
                loginC.remember.toggle();
              },
              title: Text("Remember Me"),
            ),
          ),
          SizedBox(height: 30),
          ElevatedButton(
            onPressed: () => loginC.login(),
            child: Text("LOGIN"),
            style: ElevatedButton.styleFrom(
              backgroundColor: Colors.red,
              foregroundColor: Colors.white,
              shape: RoundedRectangleBorder(
                borderRadius: BorderRadius.circular(5),
              ),
            ),
          )
        ],
      ),
    );
  }
}

```

## Home Page Code
```dart
import 'package:flutter/material.dart';
import 'package:flutter_sample/controller/login_controller.dart';
import 'package:get/get.dart';

class Home extends StatelessWidget {
  final LoginController loginC = Get.find();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Home"),
        backgroundColor: Colors.red[900],
        foregroundColor: Colors.white,
      ),
      body: Center(),
      floatingActionButton: FloatingActionButton(
        onPressed: () => loginC.logout(),
        child: Icon(Icons.logout),
      ),
    );
  }
}

```

## Controller Code for Login
```dart
import 'package:flutter/material.dart';
import 'package:flutter/widgets.dart';
import 'package:get/get.dart';
import 'package:get_storage/get_storage.dart';

class LoginController extends GetxController {
  TextEditingController emailC = TextEditingController();
  TextEditingController passC = TextEditingController();

  RxBool isHidden = true.obs;
  RxBool remember = false.obs;
  final box = GetStorage();

  void login() async {
    if (box.read("rememberStorage") != null) {
      box.remove("rememberStorage");
    }
    if (remember.isTrue) {
      //Simpan email & pass
      box.write(
        "rememberStorage",
        {"email": emailC.text, "password": passC.text},
      );
    }
    if (emailC.text == "admin@gmail.com" && passC.text == "12345") {
      Get.offAllNamed("/home");
    } else {
      Get.defaultDialog(
        title: "System",
        middleText: "Email atau Password tidak sesuai",
        onCancel: () => Text("Ok"),
      );
    }
  }

  void logout() {
    Get.offAllNamed("/login");
    Get.snackbar(
      "System",
      "Berhasil Logout",
      backgroundColor: Colors.red,
      icon: Icon(Icons.emoji_emotions),
      colorText: Colors.white,
    );
  }
}

```
