# Chat UI Flutter
```dart
import 'package:convex_bottom_bar/convex_bottom_bar.dart';
import 'package:flutter/material.dart';
import 'package:faker/faker.dart';
import 'package:intl/intl.dart';

void main() {
  var faker = new Faker();
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
  int pageSaatini = 0;

  List pageBotBar = [
    ListView.builder(
        padding: EdgeInsets.all(10),
        itemCount: 30,
        itemBuilder: (context, index) {
          String firstname = faker.person.firstName();
          String lastname = faker.person.lastName();
          String fullname = firstname + " " + lastname;
          String email =
              "${DateFormat.yMMMMEEEEd().add_Hm().format(DateTime.now())}";

          String image = "https://picsum.photos/id/${index + 22}/300/300";

          return ListTile(
            leading: CircleAvatar(
              backgroundColor: Colors.grey,
              backgroundImage: NetworkImage(image),
            ),
            title: Text(fullname),
            subtitle: Text(email),
          );
        }),
    Text("Page2"),
    Text("Page3"),
    Text("Page4"),
    Text("Page5"),
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(
          "Bottom Nav Bar",
          style: TextStyle(color: Colors.white),
        ),
        backgroundColor: Colors.green[600],
      ),
      body: pageBotBar[pageSaatini],
      bottomNavigationBar: ConvexAppBar(
        items: [
          TabItem(icon: Icons.home, title: 'Home'),
          TabItem(icon: Icons.map, title: 'Discovery'),
          TabItem(icon: Icons.add, title: 'Add'),
          TabItem(icon: Icons.message, title: 'Message'),
          TabItem(icon: Icons.people, title: 'Profile'),
        ],
        backgroundColor: Colors.green[600],
        height: 70,
        initialActiveIndex: 0,
        style: TabStyle.flip,
        onTap: (int i) {
          setState(() {
            pageSaatini = i;
          });
        },
      ),
    );
  }
}

```
