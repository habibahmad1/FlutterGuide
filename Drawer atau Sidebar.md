# Drawer atau Sidebar Flutter
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
  final List iconData = [
    {'icon': Icons.home, 'title': "Homepage"},
    {'icon': Icons.article, 'title': "Article"},
    {'icon': Icons.person, 'title': "Profile"},
    {'icon': Icons.credit_card, 'title': "Credit"},
  ];
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Drawer/Sidebar"),
        backgroundColor: Colors.purple,
      ),
      drawer: Drawer(
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Container(
              alignment: Alignment.bottomLeft,
              width: double.infinity,
              height: 150,
              color: Colors.purple,
              child: Text(
                "Dashboard",
                style: TextStyle(fontSize: 25),
              ),
              padding: EdgeInsets.all(20),
            ),
            Expanded(
                child: ListView.builder(
              itemCount: iconData.length,
              padding: EdgeInsets.zero,
              itemBuilder: (context, index) {
                return ListTile(
                  leading: Icon(iconData[index]['icon']),
                  title: Text(iconData[index]['title']),
                );
              },
            ))
          ],
        ),
      ),
      body: Text("Ok"),
    );
  }
}

```
