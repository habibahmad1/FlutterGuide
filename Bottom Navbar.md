# Bottom Navbar
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
  const Homepage({super.key});

  @override
  State<Homepage> createState() => _HomepageState();
}

class _HomepageState extends State<Homepage> {
  int btNavbar = 0;
  List page = [
    Center(
      child: Text("Home"),
    ),
    Center(
      child: Text("Menu"),
    ),
    Center(
      child: Text("Cart"),
    ),
    Center(
      child: Text("Message"),
    ),
    Center(
      child: Text("Profil"),
    ),
  ];
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(
          "Bottom Navbar",
          style: TextStyle(color: Colors.white),
        ),
        backgroundColor: Color(0xFF252525),
      ),
      body: page[btNavbar],
      bottomNavigationBar: BottomNavigationBar(
          type: BottomNavigationBarType.fixed,
          currentIndex: btNavbar,
          selectedItemColor: Colors.white,
          showUnselectedLabels: false,
          unselectedItemColor: Colors.grey[500],
          iconSize: 28,
          onTap: (value) {
            setState(() {
              btNavbar = value;
            });
          },
          backgroundColor: Colors.black,
          items: [
            BottomNavigationBarItem(icon: Icon(Icons.home), label: "Home"),
            BottomNavigationBarItem(
                icon: Icon(Icons.local_pizza), label: "Menu"),
            BottomNavigationBarItem(
                icon: Icon(Icons.shopping_cart), label: "Cart"),
            BottomNavigationBarItem(
                icon: Icon(Icons.message), label: "Message"),
            BottomNavigationBarItem(icon: Icon(Icons.person), label: "Profil"),
          ]),
    );
  }
}

```
