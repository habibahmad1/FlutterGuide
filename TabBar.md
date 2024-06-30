# TabBar Flutter
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

class _HomepageState extends State<Homepage>
    with SingleTickerProviderStateMixin {
  late TabController tabC = TabController(length: 3, vsync: this);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Tab Bar"),
        backgroundColor: Colors.green,
        bottom: TabBar(
            controller: tabC,
            indicatorColor: Colors.teal,
            labelColor: Colors.white,
            dividerColor: Colors.green,
            tabs: [
              Tab(
                icon: Icon(Icons.camera),
                text: "Camera",
              ),
              Tab(
                icon: Icon(Icons.message),
                text: "Message",
              ),
              Tab(
                icon: Icon(Icons.phone),
                text: "Calls",
              ),
            ]),
      ),
      body: TabBarView(controller: tabC, children: [
        ListView.builder(
          itemCount: 5,
          itemBuilder: (context, index) {
            return Container(
              height: 70,
              color: index % 2 == 0 ? Colors.grey[300] : Colors.grey,
            );
          },
        ),
        GridView.builder(
          padding: EdgeInsets.symmetric(vertical: 20, horizontal: 10),
          gridDelegate: SliverGridDelegateWithFixedCrossAxisCount(
              crossAxisCount: 3, crossAxisSpacing: 10, mainAxisSpacing: 10),
          itemCount: 20,
          itemBuilder: (context, index) {
            return Container(
              height: 70,
              color: index % 2 == 0 ? Colors.red[300] : Colors.red,
            );
          },
        ),
        SingleChildScrollView(
          child: Column(children: [
            Container(
              alignment: Alignment.centerLeft,
              padding: EdgeInsets.symmetric(horizontal: 20),
              width: double.infinity,
              height: 70,
              color: Colors.pink[100],
              child: Text("My Mom"),
            ),
            Container(
              alignment: Alignment.centerLeft,
              padding: EdgeInsets.symmetric(horizontal: 20),
              width: double.infinity,
              height: 70,
              color: Colors.pink,
              child: Text("My Dad"),
            ),
            Container(
              alignment: Alignment.centerLeft,
              padding: EdgeInsets.symmetric(horizontal: 20),
              width: double.infinity,
              height: 70,
              color: Colors.pink[100],
              child: Text("My Sister"),
            ),
          ]),
        ),
      ]),
    );
  }
}

```
