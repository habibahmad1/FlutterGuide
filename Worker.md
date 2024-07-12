# Worker FLutter
## Ini Controller
```dart
import 'package:get/get.dart';

class homeControl extends GetxController {
  RxInt data = 0.obs;

  void change() => data++;

  @override
  void onInit() {
    //! untuk terus pantau
    // ever(data, (e) => print("Ok"));
    //
    //! sekali pantau
    // once(data, (e) => print("Ok"));

    //! Setelah selesai ada perubahan baru di pantau
    // debounce(data, (e) => print("Ok"), time: Duration(seconds: 2));

    //! akan di eksekusi saat perubahan berlangsung dan saat selesai jika pakai time
    // debounce(data, (e) => print("Ok"), time: Duration(seconds: 2));

    super.onInit();
  }
}

```

## Main Code
```dart
import 'package:flutter/material.dart';
import '../Controller/homeControl.dart';
import 'package:get/get.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return GetMaterialApp(
      debugShowCheckedModeBanner: false,
      home: Homepage(),
    );
  }
}

class Homepage extends StatelessWidget {
  final homeC = Get.put(homeControl());

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Worker"),
        backgroundColor: Colors.purple,
        foregroundColor: Colors.white,
      ),
      body: Padding(
        padding: EdgeInsets.all(20),
        child: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              Obx(
                () => Text(
                  "Telah di Ubah ke : ${homeC.data}x",
                  style: TextStyle(
                    fontSize: 22,
                    color: Colors.red,
                    fontWeight: FontWeight.bold,
                  ),
                ),
              ),
              SizedBox(height: 30),
              TextField(
                onChanged: (value) => homeC.change(),
                decoration: InputDecoration(
                  label: Text("Name"),
                  border: OutlineInputBorder(),
                ),
              )
            ],
          ),
        ),
      ),
    );
  }
}

```
