# Source Code untuk Doa APK Flutter
Ini masih belum menggunakan GetX Pattern/Framework


### 1. Buat project untuk flutter
```dart
flutter create doa
```

### 2. Didalam folder libs buat folder models lalu buat file doa.dart, isi ini dibuat dengan quicktype untuk data json.
```dart
// To parse this JSON data, do
//
//     final doaList = doaListFromJson(jsonString);

import 'dart:convert';

List<DoaList> doaListFromJson(String str) =>
    List<DoaList>.from(json.decode(str).map((x) => DoaList.fromJson(x)));

String doaListToJson(List<DoaList> data) =>
    json.encode(List<dynamic>.from(data.map((x) => x.toJson())));

class DoaList {
  String id;
  String doa;
  String ayat;
  String latin;
  String artinya;

  DoaList({
    required this.id,
    required this.doa,
    required this.ayat,
    required this.latin,
    required this.artinya,
  });

  factory DoaList.fromJson(Map<String, dynamic> json) => DoaList(
        id: json["id"],
        doa: json["doa"],
        ayat: json["ayat"],
        latin: json["latin"],
        artinya: json["artinya"],
      );

  Map<String, dynamic> toJson() => {
        "id": id,
        "doa": doa,
        "ayat": ayat,
        "latin": latin,
        "artinya": artinya,
      };
}

```

### 3. Main Code dengan page dipisah jadi pada main code awal tampilkan home. Jangan lupa import homepage.
```dart
import 'package:flutter/material.dart';

import './pages/homepage.dart';

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

```

### 4. Homepage Code
```dart
import 'dart:convert';

import 'package:flutter/material.dart';
import '../my widgets/carddoa.dart';
import 'package:http/http.dart' as myhttp;

import '../models/doa.dart';

class Homepage extends StatefulWidget {
  const Homepage({super.key});

  @override
  State<Homepage> createState() => _HomepageState();
}

class _HomepageState extends State<Homepage> {
  List<DoaList> dataDoa = [];

  Future getDataDoa() async {
    var url = Uri.parse("https://doa-doa-api-ahmadramadhan.fly.dev/api");
    var respon = await myhttp.get(url);

    if (respon.statusCode == 200) {
      List<dynamic> data = jsonDecode(respon.body);

      dataDoa = data.map((item) => DoaList.fromJson(item)).toList();
    } else {
      print("No Data");
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(
          "Doa Harian",
          style: TextStyle(color: Colors.white),
        ),
        backgroundColor: Colors.purple,
      ),
      body: FutureBuilder(
          future: getDataDoa(),
          builder: (context, snapshot) {
            if (snapshot.connectionState == ConnectionState.waiting) {
              return Center(
                child: Column(
                  mainAxisAlignment: MainAxisAlignment.center,
                  children: [
                    Icon(Icons.wifi),
                    Text("Loading"),
                  ],
                ),
              );
            }
            return ListView.builder(
              itemCount: dataDoa.length,
              itemBuilder: (context, index) {
                return CardDoa(
                  dataDoa[index].ayat,
                  dataDoa[index].doa,
                );
              },
            );
          }),
    );
  }
}

```


### 5. Buat folder widget untuk taruh widget yang telah di ekstrak pada folder widget dengan nama carddoa.dart.
```dart
import 'package:flutter/material.dart';

class CardDoa extends StatelessWidget {
  CardDoa(this.namaDoa, this.ayatDoa);

  String namaDoa;
  String ayatDoa;

  @override
  Widget build(BuildContext context) {
    return Card(
      margin: EdgeInsets.all(20),
      elevation: 5,
      shape: RoundedRectangleBorder(borderRadius: BorderRadius.circular(12)),
      child: SingleChildScrollView(
        child: Container(
          height: 300,
          width: double.infinity,
          decoration: BoxDecoration(
              color: Colors.purple[200],
              borderRadius: BorderRadius.circular(12)),
          child: Center(
            child: Padding(
              padding: const EdgeInsets.all(20),
              child: Column(
                mainAxisAlignment: MainAxisAlignment.center,
                children: [
                  Text(
                    namaDoa,
                    style: TextStyle(
                        fontSize: 22,
                        color: Colors.black,
                        fontWeight: FontWeight.bold),
                    textAlign: TextAlign.right,
                  ),
                  SizedBox(height: 20),
                  Text(
                    ayatDoa,
                    style: TextStyle(
                      color: Colors.white,
                      fontSize: 20,
                    ),
                    textAlign: TextAlign.center,
                  ),
                ],
              ),
            ),
          ),
        ),
      ),
    );
  }
}

```
