# Form Login Flutter

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
      home: HomePage(),
    );
  }
}

class HomePage extends StatefulWidget {
  const HomePage({super.key});

  @override
  State<HomePage> createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  bool mata = true;
  TextEditingController emailC = TextEditingController();
  TextEditingController passC = TextEditingController();
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Text Field"),
        backgroundColor: Colors.orange,
      ),
      body: ListView(
        padding: EdgeInsets.all(20),
        children: [
          Center(
              child: Padding(
            padding: const EdgeInsets.only(top: 20, bottom: 40),
            child: Text(
              "Masuk ke Akun Anda",
              style: TextStyle(fontSize: 26),
            ),
          )),
          TextField(
            controller: emailC,
            autocorrect: false,
            textInputAction: TextInputAction.next,
            keyboardType: TextInputType.emailAddress,
            decoration: InputDecoration(
                label: Text("Your Email"),
                border: OutlineInputBorder(
                    borderRadius: BorderRadius.circular(100)),
                contentPadding:
                    EdgeInsets.symmetric(horizontal: 20, vertical: 10),
                prefixIcon: Icon(Icons.email)),
          ),
          SizedBox(height: 20),
          TextField(
            controller: passC,
            autocorrect: false,
            obscureText: mata,
            decoration: InputDecoration(
                label: Text("Your Password"),
                border: OutlineInputBorder(
                    borderRadius: BorderRadius.circular(100)),
                contentPadding:
                    EdgeInsets.symmetric(horizontal: 20, vertical: 10),
                prefixIcon: Icon(Icons.password),
                suffixIcon: IconButton(
                    onPressed: () {
                      if (mata == true) {
                        mata = false;
                      } else {
                        mata = true;
                      }
                      setState(() {});
                    },
                    icon: Icon(Icons.remove_red_eye))),
          ),
          Center(
            child: Padding(
              padding: const EdgeInsets.all(40),
              child: ElevatedButton(
                onPressed: () {
                  print(
                      "Your Email: ${emailC.text} and Password: ${passC.text}");
                },
                child: Text("Login"),
                style: ElevatedButton.styleFrom(
                  padding: EdgeInsets.symmetric(horizontal: 100),
                  backgroundColor: Colors.red,
                  foregroundColor: Colors.white,
                  shape: RoundedRectangleBorder(
                      borderRadius: BorderRadius.circular(20)),
                ),
              ),
            ),
          )
        ],
      ),
    );
  }
}

```
