# Http Request FLutter
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
  late String id;
  late String email;
  late String name;

  @override
  void initState() {
    // TODO: implement initState
    id = "";
    email = "";
    name = "";
    super.initState();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Http Get"),
        backgroundColor: Colors.blue,
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text(
              "ID : $id",
              style: TextStyle(fontSize: 22),
            ),
            Text(
              "Email : $email",
              style: TextStyle(fontSize: 22),
            ),
            Text(
              "Name : $name",
              style: TextStyle(fontSize: 22),
            ),
            ElevatedButton(
              onPressed: () async {
                var myData = await myhttp
                    .get(Uri.parse("https://reqres.in/api/users/7"));

                if (myData.statusCode == 200) {
                  //Berhasil
                  var data = json.decode(myData.body) as Map<String, dynamic>;
                  setState(() {
                    id = data["data"]["id"].toString();
                    email = data["data"]["email"].toString();
                    name =
                        "${data["data"]["first_name"].toString()} ${data["data"]["last_name"].toString()}";
                  });
                } else {
                  setState(() {
                    print("Error ${myData.statusCode}");
                  });
                }
              },
              child: Text("Get Data"),
            ),
          ],
        ),
      ),
    );
  }
}

```
