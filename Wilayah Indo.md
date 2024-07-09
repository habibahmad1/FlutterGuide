# Wilayah Indo Flutter
```dart
import 'dart:convert';

import 'package:flutter/material.dart';
import 'package:dropdown_search/dropdown_search.dart';
import 'package:flutter_sample/model/City.dart';
import 'package:flutter_sample/model/CityModel.dart';
import 'package:http/http.dart' as myhttp;

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
  String? idprov;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("API Wilayah Indonesia"),
        backgroundColor: Colors.blue[600],
      ),
      body: ListView(
        padding: EdgeInsets.all(20),
        children: [
          DropdownSearch<CityModel>(
            compareFn: (item, selectedItem) => item == selectedItem,
            dropdownBuilder: (context, selectedItem) =>
                Text(selectedItem?.name ?? "Pilih Wilayah"),
            itemAsString: (CityModel u) => u.name,
            asyncItems: (test) async {
              var response = await myhttp.get(Uri.parse(
                  "https://www.emsifa.com/api-wilayah-indonesia/api/provinces.json"));
              if (response.statusCode != 200) {
                return [];
              }

              List data = jsonDecode(response.body);

              List<CityModel> dataSatuan = [];

              data.forEach((e) {
                dataSatuan.add(CityModel(id: e['id'], name: e['name']));
              });

              return dataSatuan;
            },
            popupProps: PopupProps.dialog(
              showSearchBox: true,
              showSelectedItems: true,
            ),
            dropdownDecoratorProps: DropDownDecoratorProps(
              dropdownSearchDecoration: InputDecoration(
                labelText: "Menu mode",
                hintText: "country in menu mode",
              ),
            ),
            onChanged: (value) => idprov = value?.id,
          ),
          SizedBox(height: 30),
          DropdownSearch<City>(
            compareFn: (item, selectedItem) => item == selectedItem,
            dropdownBuilder: (context, selectedItem) =>
                Text(selectedItem?.name ?? "Pilih Wilayah"),
            itemAsString: (City u) => u.name,
            asyncItems: (test) async {
              var response = await myhttp.get(Uri.parse(
                  "https://www.emsifa.com/api-wilayah-indonesia/api/regencies/$idprov.json"));
              if (response.statusCode != 200) {
                return [];
              }

              List data = jsonDecode(response.body);

              List<City> dataSatuan = [];

              data.forEach((e) {
                dataSatuan.add(City(
                    id: e['id'],
                    provinceId: e['province_id'],
                    name: e['name']));
              });

              return dataSatuan;
            },
            popupProps: PopupProps.dialog(
              showSearchBox: true,
              showSelectedItems: true,
            ),
            dropdownDecoratorProps: DropDownDecoratorProps(
              dropdownSearchDecoration: InputDecoration(
                labelText: "Menu mode",
                hintText: "country in menu mode",
              ),
            ),
            onChanged: (value) => print(value?.toJson()),
          ),
        ],
      ),
    );
  }
}

```
