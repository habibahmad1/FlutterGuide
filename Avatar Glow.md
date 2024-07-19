# Avatar Glow Flutter
Merupakan agar ada seperti animasi notif
```dart
import 'package:flutter/material.dart';
import 'package:avatar_glow/avatar_glow.dart';

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

class Homepage extends StatelessWidget {
  const Homepage({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Avatar Glow"),
        backgroundColor: Colors.orange[200],
      ),
      body: ListView.builder(
        padding: EdgeInsets.all(10),
        itemCount: 5,
        itemBuilder: (context, index) {
          return ListTile(
            onTap: () => print("$index"),
            leading: AvatarGlow(
              child: Material(
                shape: CircleBorder(),
                child: CircleAvatar(
                  radius: 12.0,
                  backgroundImage:
                      NetworkImage("https://picsum.photos/300/300"),
                ),
              ),
              glowColor: Colors.red,
              glowCount: 2,
              glowShape: BoxShape.circle,
            ),
            title: Text("Name Person ${index + 1}"),
          );
        },
      ),
    );
  }
}

```
