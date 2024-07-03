# Instagram UI Design FLutter
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
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Row(
          children: [
            Text(
              "Habib Ahmad",
              style: TextStyle(fontWeight: FontWeight.bold),
            ),
            Icon(Icons.arrow_drop_down)
          ],
        ),
        actions: [
          IconButton(onPressed: () {}, icon: Icon(Icons.add_box_outlined)),
          IconButton(onPressed: () {}, icon: Icon(Icons.menu)),
        ],
      ),
      body: ListView(
        children: [
          Row(
            children: [
              Stack(
                alignment: Alignment.center,
                children: [
                  Container(
                    width: 100,
                    height: 100,
                    margin: EdgeInsets.only(left: 20),
                    decoration: BoxDecoration(
                        gradient: LinearGradient(
                            begin: Alignment.topCenter,
                            end: Alignment.bottomCenter,
                            colors: [Colors.red, Colors.amber]),
                        borderRadius: BorderRadius.circular(60)),
                  ),
                  Container(
                    width: 90,
                    height: 90,
                    margin: EdgeInsets.only(left: 20),
                    decoration: BoxDecoration(
                        image: DecorationImage(
                            image:
                                NetworkImage("https://picsum.photos/300/300"),
                            fit: BoxFit.cover),
                        color: Colors.grey,
                        border: Border.all(color: Colors.white, width: 4),
                        borderRadius: BorderRadius.circular(60)),
                  ),
                ],
              ),
              const Expanded(
                child: Row(
                  mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                  children: [
                    Followers(jumlahData: "220", infoData: "Posts"),
                    Followers(jumlahData: "124K", infoData: "Followers"),
                    Followers(jumlahData: "3", infoData: "Following"),
                  ],
                ),
              ),
            ],
          ),
          Padding(
            padding: EdgeInsets.only(top: 20, left: 20),
            child: Text(
              "Habib",
              style: TextStyle(fontSize: 16, fontWeight: FontWeight.bold),
            ),
          ),
          Padding(
            padding: EdgeInsets.symmetric(horizontal: 20),
            child: RichText(
              text: TextSpan(
                  text:
                      "Lorem ipsum dolor sit amet consectetur adipiscing elit feugiat platea, venenatis curae netus cursus per ac tempor libero, nullam pellentesque",
                  style: TextStyle(color: Colors.black),
                  children: [
                    TextSpan(
                      text: " #Influencer #Gamer #Programmer",
                      style: TextStyle(color: Colors.blue[600]),
                    ),
                  ]),
            ),
          ),
          Padding(
            padding: EdgeInsets.symmetric(horizontal: 20, vertical: 10),
            child: Text(
              "Https://Youtube.com/habibahmad",
              style: TextStyle(
                  color: Colors.blue[900], fontStyle: FontStyle.italic),
            ),
          ),
          Padding(
            padding: EdgeInsets.symmetric(horizontal: 20),
            child: OutlinedButton(
              onPressed: () {},
              child: Text(
                "Edit Profile",
                style: TextStyle(color: Colors.black),
              ),
              style: OutlinedButton.styleFrom(
                shape: RoundedRectangleBorder(
                  borderRadius: BorderRadius.circular(5),
                ),
              ),
            ),
          )
        ],
      ),
    );
  }
}

class Followers extends StatelessWidget {
  final String? jumlahData;
  final String? infoData;
  const Followers({
    super.key,
    required this.jumlahData,
    required this.infoData,
  });

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Text(
          jumlahData.toString(),
          style: TextStyle(fontSize: 20, fontWeight: FontWeight.bold),
        ),
        Text(infoData.toString()),
      ],
    );
  }
}

```
