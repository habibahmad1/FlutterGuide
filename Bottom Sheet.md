# Bottom Sheet Flutter
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
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(
          "Bottom Sheet",
          style: TextStyle(color: Colors.white),
        ),
        backgroundColor: Color(0xFF252525),
      ),
      body: Center(
        child: Padding(
          padding: EdgeInsets.all(30),
          child: ElevatedButton(
              onPressed: () {
                showModalBottomSheet(
                  isDismissible: false,
                  backgroundColor: Colors.blueAccent,
                  context: context,
                  builder: (context) => Container(
                    height: 300,
                    child: Center(
                      child: ListView(
                        children: [
                          ListTile(
                            leading: Icon(Icons.photo_album),
                            title: Text("Photos"),
                          ),
                          ListTile(
                            leading: Icon(Icons.video_collection),
                            title: Text("Videos"),
                          ),
                          ListTile(
                            leading: Icon(Icons.music_note),
                            title: Text("Music"),
                          ),
                          ListTile(
                            leading: Icon(Icons.close),
                            title: Text("Tutup"),
                            onTap: () {
                              Navigator.pop(context);
                            },
                          ),
                        ],
                      ),
                    ),
                    decoration: BoxDecoration(
                      borderRadius:
                          BorderRadius.vertical(top: Radius.circular(10)),
                      // color: Colors.pink,
                    ),
                  ),
                );
              },
              child: Text("Buka Sheet")),
        ),
      ),
    );
  }
}

```
