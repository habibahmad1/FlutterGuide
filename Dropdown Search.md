# Dropdown Search.md
```dart
import 'package:flutter/material.dart';
import 'package:dropdown_search/dropdown_search.dart';

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
  @override
  State<Homepage> createState() => _HomepageState();
}

class _HomepageState extends State<Homepage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Dropdown Search"),
        backgroundColor: Colors.blue[600],
      ),
      body: Padding(
        padding: const EdgeInsets.all(20),
        child: DropdownSearch(
          popupProps: PopupProps.menu(
            showSearchBox: true,
            showSelectedItems: true,
            disabledItemFn: (String s) => s.startsWith('Z'),
          ),
          items: [
            "Australia",
            "Korea",
            "Jepang",
            "Indonesia",
            "China",
            "Zimbabwe",
            "Firlandia",
            "Polland",
            "German"
          ],
          dropdownDecoratorProps: DropDownDecoratorProps(
            dropdownSearchDecoration: InputDecoration(
              labelText: "Your Country",
              hintText: "country in menu mode",
            ),
          ),
          onChanged: print,
          selectedItem: "Jepang",
          clearButtonProps:
              ClearButtonProps(isVisible: true, color: Colors.red),
        ),
      ),
    );
  }
}

```
