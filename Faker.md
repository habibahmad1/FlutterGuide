# Faker FLutter
untuk buat data dummy/palsu
```dart
import 'package:flutter/material.dart';
import 'package:faker/faker.dart';

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
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Faker"),
        backgroundColor: Colors.green[600],
      ),
      body: ListView.builder(
          padding: EdgeInsets.all(10),
          itemCount: 30,
          itemBuilder: (context, index) {
            String firstname = faker.person.firstName();
            String lastname = faker.person.lastName();
            String fullname = firstname + " " + lastname;
            String email = "${firstname}.${lastname}@gmail.com";

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
    );
  }
}

```
