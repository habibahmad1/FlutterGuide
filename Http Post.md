# Http Post Flutter
```dart
import 'dart:convert';

import 'package:flutter/material.dart';
import 'package:http/http.dart' as myhttp;

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
      home: HomePage(),
    );
  }
}

class HomePage extends StatefulWidget {
  const HomePage({super.key});

  @override
  State<HomePage> createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  TextEditingController nameC = TextEditingController();
  TextEditingController jobC = TextEditingController();

  String responAwal = "No Data";

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Http Post"),
        backgroundColor: Colors.green,
      ),
      body: ListView(
        padding: EdgeInsets.all(20),
        children: [
          Padding(
            padding: const EdgeInsets.only(bottom: 20),
            child: Text(
              "Input User",
              style: TextStyle(fontSize: 26),
              textAlign: TextAlign.center,
            ),
          ),
          TextField(
            controller: nameC,
            keyboardType: TextInputType.text,
            autofocus: true,
            decoration: InputDecoration(
                label: Text("Name"), border: OutlineInputBorder()),
          ),
          SizedBox(height: 20),
          TextField(
            controller: jobC,
            keyboardType: TextInputType.text,
            autofocus: true,
            decoration: InputDecoration(
                label: Text("Job"), border: OutlineInputBorder()),
          ),
          SizedBox(height: 20),
          ElevatedButton(
            onPressed: () async {
              var database = await myhttp.post(
                Uri.parse("https://reqres.in/api/users"),
                body: {"name": nameC.text, "job": jobC.text},
              );

              Map<String, dynamic> data = jsonDecode(database.body);

              setState(() {
                responAwal = "${data['name']} ==== ${data['job']}";
              });
            },
            child: Text("Add User"),
            style: ElevatedButton.styleFrom(
                backgroundColor: Colors.amber,
                shape: RoundedRectangleBorder(
                    borderRadius: BorderRadius.circular(6))),
          ),
          SizedBox(height: 20),
          Divider(
            color: Colors.red[600],
          ),
          Text(responAwal),
        ],
      ),
    );
  }
}

```
