# Future Builder FLutter
```dart
import 'dart:convert';

import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
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
  List<dynamic> dataCollect = [];
  Future getUser() async {
    try {
      var uriData = Uri.parse("https://reqres.in/api/users");
      var respon = await http.get(uriData);
      var getData = jsonDecode(respon.body);
      List<dynamic> data = getData['data'];

      data.forEach((e) {
        dataCollect.add(e);
      });
    } catch (e) {
      print("Error $e");
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Future Builder"),
        backgroundColor: Color(0xffef476f),
      ),
      body: FutureBuilder(
          future: getUser(),
          builder: (context, snapshot) {
            if (snapshot.connectionState == ConnectionState.waiting) {
              return Center(
                child: Text("Loading Mas Bro ..."),
              );
            } else {
              return ListView.builder(
                itemCount: dataCollect.length,
                itemBuilder: (context, index) {
                  return ListTile(
                    leading: CircleAvatar(
                      backgroundColor: Colors.grey[600],
                      backgroundImage:
                          NetworkImage("${dataCollect[index]['avatar']}"),
                    ),
                    title: Text(
                        "Name: ${dataCollect[index]['first_name']} ${dataCollect[index]['last_name']}"),
                    subtitle: Text("Email: ${dataCollect[index]['email']}"),
                  );
                },
              );
            }
          }),
    );
  }
}

```
