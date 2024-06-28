# Snackbar Flutter
```dart
  import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: HomePage(),
    );
  }
}

class HomePage extends StatelessWidget {
  const HomePage({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Snackbar"),
        backgroundColor: Colors.amber,
        leading: FlutterLogo(),
      ),
      body: Center(
        child: ElevatedButton(
            onPressed: () {
              ScaffoldMessenger.of(context).showSnackBar(SnackBar(
                content: Text(
                  "Teks telah dihapus",
                  style: TextStyle(color: Colors.white),
                ),
                action: SnackBarAction(
                  label: "Urungkan",
                  onPressed: () {},
                  textColor: Colors.white,
                  backgroundColor: Colors.grey,
                ),
                backgroundColor: Colors.black,
                duration: Duration(seconds: 3),
                margin: EdgeInsets.all(20),
                behavior: SnackBarBehavior.floating,
              ));
            },
            child: Text("Snackbar")),
      ),
    );
  }
}


```
