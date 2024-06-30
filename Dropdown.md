# Dropdown Flutter
```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatefulWidget {
  const MyApp({super.key});

  @override
  State<MyApp> createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Homepage(),
    );
  }
}

class Homepage extends StatefulWidget {
  @override
  State<Homepage> createState() => _HomepageState();
}

class _HomepageState extends State<Homepage> {
  final List<String> buah = ["Melon", "Pepaya", "Jambu", "Leci"];

  String? selectedBuah;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Dropdown"),
        backgroundColor: Colors.orange,
      ),
      body: Center(
        child: Padding(
          padding: EdgeInsets.all(20),
          child: DropdownButton(
            value: selectedBuah,
            hint: Text("Pilih Buah Anda"),
            items: buah.map((value) {
              return DropdownMenuItem(
                value: value,
                child: Text("Buah ${value}"),
              );
            }).toList(),
            onChanged: (newValue) {
              setState(() {
                selectedBuah = newValue;
              });
            },
          ),
        ),
      ),
    );
  }
}

```
