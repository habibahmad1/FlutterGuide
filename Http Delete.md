# Http Delete FLutter
```dart
import 'dart:convert';

import 'package:flutter/material.dart';
import 'package:http/http.dart' as myhttp;

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Homepage(),
    );
  }
}

class Homepage extends StatefulWidget {
  const Homepage({super.key});

  @override
  State<Homepage> createState() => _HomepageState();
}

class _HomepageState extends State<Homepage> {
  String getData = "Belum Ada Data";
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Http Delete"),
        backgroundColor: Color(0XFF06d6a0),
        actions: [
          IconButton(
            onPressed: () async {
              var respon =
                  await myhttp.get(Uri.parse("https://reqres.in/api/users/2"));
              Map<String, dynamic> getDataServer = jsonDecode(respon.body);

              setState(() {
                getData =
                    "Nama : ${getDataServer['data']['first_name']} ${getDataServer['data']['last_name']}";
              });
            },
            icon: Icon(Icons.get_app),
          )
        ],
      ),
      body: ListView(
        padding: EdgeInsets.all(20),
        children: [
          Text(getData),
          SizedBox(height: 30),
          ElevatedButton(
            onPressed: () async {
              var responDel = await myhttp
                  .delete(Uri.parse("https://reqres.in/api/users/2"));
              if (responDel.statusCode == 204) {
                setState(() {
                  getData = "Berhasil Hapus Data";
                });
              }
            },
            child: Text("Delete"),
            style: ElevatedButton.styleFrom(
                shape: RoundedRectangleBorder(
                    borderRadius: BorderRadius.circular(0)),
                backgroundColor: Colors.blue[200]),
          )
        ],
      ),
    );
  }
}

```
