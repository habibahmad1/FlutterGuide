# Source Code Ongkir Flutter APK
### 1. Buat project flutter
```dart
flutter create ongkir
```

### 2. Buat project menjadi menggunakan Get Pattern, ketik di terminal dalam project.
```dart
get init
```

### 3. Buat sebuah folder baru untuk menyimpan model yang digunakan, buat pada root dengan nama folder assets/models/kota.json.
```dart
{
  "city_id": "39",
  "province_id": "5",
  "province": "DI Yogyakarta",
  "type": "Kabupaten",
  "city_name": "Bantul",
  "postal_code": "55700"
}
```

### 4. Buat file lagi di models dengan nama ongkir.json.
```dart
{
  "service": "OKE",
  "description": "Ongkos Kirim Ekonomis",
  "cost": [
    {
      "value": 38000,
      "etd": "4-5",
      "note": ""
    }
  ]
}
```

### 5. Buat file lagi di models dengan nama provinsi.json.
```dart
{
  "province_id": "12",
  "province": "Kalimantan Barat"
}
```

### 6. Buat file moodels dengan pattern GetX, dengan cara ketik di terminal.
```dart
get generate models with assets/models/kota.json --skipProvider
```

### 7. Buat untuk Provinsi dan Ongkir juga.
### 8. Setelah dibuat akan berada di App/data/models/kota_model.json secara otomatis sudah dibuat ada 3 yaitu untuk provinsi,kota,ongkir model.
### 9. Tambahkan kode ini pada kota dan provinsi model untuk konversi JSON ke List. Ganti Kota dengan Provinsi jika di model provinsi
```dart
static List<Kota> fromJsonList(List? data) {
    if (data == null || data.length == 0) return [];
    return data.map((e) => Kota.fromJson(e)).toList();
  }

  @override
  String toString() => cityName!;
```

### 10. Code untuk tampilan aplikasi
```dart
import 'package:flutter/material.dart';

import 'package:get/get.dart';
import 'package:ongkir/app/data/models/kota_model.dart';
import 'package:ongkir/app/data/models/provinsi_model.dart';

import '../controllers/home_controller.dart';

import 'package:dropdown_search/dropdown_search.dart';

import 'package:dio/dio.dart';

class HomeView extends GetView<HomeController> {
  const HomeView({Key? key}) : super(key: key);
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Ongkos Kirim'),
        centerTitle: true,
        backgroundColor: Colors.green[600],
        foregroundColor: Colors.white,
      ),
      body: ListView(
        padding: EdgeInsets.all(20),
        children: [
          DropdownSearch<Provinsi>(
            popupProps: PopupProps.dialog(
              showSearchBox: true,
            ),
            asyncItems: (String filter) async {
              var response = await Dio().get(
                "https://api.rajaongkir.com/starter/province",
                queryParameters: {"key": "59437d1d50e23a94d13e440f8ad72cb1"},
              );
              var models =
                  Provinsi.fromJsonList(response.data['rajaongkir']['results']);
              return models;
            },
            itemAsString: (Provinsi provinsi) => provinsi.province ?? '',
            onChanged: (Provinsi? data) {
              controller.provinsiAsalId.value =
                  int.parse(data?.provinceId ?? '0');
            },
            dropdownDecoratorProps: DropDownDecoratorProps(
              dropdownSearchDecoration: InputDecoration(
                  labelText: "Nama Provinsi",
                  contentPadding: EdgeInsets.symmetric(
                    vertical: 10,
                    horizontal: 15,
                  ),
                  border: OutlineInputBorder()),
            ),
          ),
          SizedBox(height: 20),
          DropdownSearch<Kota>(
            popupProps: PopupProps.dialog(
              showSearchBox: true,
            ),
            asyncItems: (String filter) async {
              var response = await Dio().get(
                "https://api.rajaongkir.com/starter/city?province=${controller.provinsiAsalId}",
                queryParameters: {"key": "59437d1d50e23a94d13e440f8ad72cb1"},
              );
              var modelsCity =
                  Kota.fromJsonList(response.data['rajaongkir']['results']);
              return modelsCity;
            },
            itemAsString: (Kota kota) =>
                '${kota.type} ${kota.cityName} (${kota.postalCode})',
            onChanged: (Kota? data) {
              controller.kotaAsalId.value = int.parse(data?.cityId ?? '0');
            },
            dropdownDecoratorProps: DropDownDecoratorProps(
              dropdownSearchDecoration: InputDecoration(
                  labelText: "Nama Kota",
                  contentPadding: EdgeInsets.symmetric(
                    vertical: 10,
                    horizontal: 15,
                  ),
                  border: OutlineInputBorder()),
            ),
          ),
          SizedBox(height: 20),
          DropdownSearch<Provinsi>(
            popupProps: PopupProps.dialog(
              showSearchBox: true,
            ),
            asyncItems: (String filter) async {
              var response = await Dio().get(
                "https://api.rajaongkir.com/starter/province",
                queryParameters: {"key": "59437d1d50e23a94d13e440f8ad72cb1"},
              );
              var models =
                  Provinsi.fromJsonList(response.data['rajaongkir']['results']);
              return models;
            },
            itemAsString: (Provinsi provinsi) => provinsi.province ?? '',
            onChanged: (Provinsi? data) {
              controller.provinsiTujuanAsalId.value =
                  int.parse(data?.provinceId ?? '0');
            },
            dropdownDecoratorProps: DropDownDecoratorProps(
              dropdownSearchDecoration: InputDecoration(
                  labelText: "Provinsi Tujuan",
                  contentPadding: EdgeInsets.symmetric(
                    vertical: 10,
                    horizontal: 15,
                  ),
                  border: OutlineInputBorder()),
            ),
          ),
          SizedBox(height: 20),
          DropdownSearch<Kota>(
            popupProps: PopupProps.dialog(
              showSearchBox: true,
            ),
            asyncItems: (String filter) async {
              var response = await Dio().get(
                "https://api.rajaongkir.com/starter/city?province=${controller.provinsiTujuanAsalId}",
                queryParameters: {"key": "59437d1d50e23a94d13e440f8ad72cb1"},
              );
              var modelsCity =
                  Kota.fromJsonList(response.data['rajaongkir']['results']);
              return modelsCity;
            },
            itemAsString: (Kota kota) =>
                '${kota.type} ${kota.cityName} (${kota.postalCode})',
            onChanged: (Kota? data) {
              controller.kotaTujuanAsalId.value =
                  int.parse(data?.cityId ?? '0');
            },
            dropdownDecoratorProps: DropDownDecoratorProps(
              dropdownSearchDecoration: InputDecoration(
                  labelText: "Kota Tujuan",
                  contentPadding: EdgeInsets.symmetric(
                    vertical: 10,
                    horizontal: 15,
                  ),
                  border: OutlineInputBorder()),
            ),
          ),
          SizedBox(height: 20),
          DropdownSearch<Map<String, dynamic>>(
            popupProps: PopupProps.dialog(
              showSearchBox: true,
            ),
            dropdownDecoratorProps: DropDownDecoratorProps(
              dropdownSearchDecoration: InputDecoration(
                  labelText: "Jasa Kirim",
                  contentPadding: EdgeInsets.symmetric(
                    vertical: 10,
                    horizontal: 15,
                  ),
                  border: OutlineInputBorder()),
            ),
            itemAsString: (kurir) => '${kurir['kurir']}',
            items: [
              {
                "code": "jne",
                "kurir": "JNE",
              },
              {
                "code": "pos",
                "kurir": "Pos Indonesia",
              },
              {
                "code": "tiki",
                "kurir": "TIKI",
              },
            ],
            dropdownBuilder: (context, selectedItem) => Text(
              "${selectedItem?['kurir'] ?? "Pilih Kurir"}",
            ),
            onChanged: (data) => controller.kurirId.value = data?['code'] ?? '',
          ),
          SizedBox(height: 20),
          TextField(
            decoration: InputDecoration(
              labelText: "Berat Barang (gram)",
              border: OutlineInputBorder(),
              contentPadding:
                  EdgeInsets.symmetric(vertical: 10, horizontal: 15),
            ),
            keyboardType: TextInputType.number,
            controller: controller.beratC,
          ),
          SizedBox(height: 20),
          ElevatedButton(
            onPressed: () => controller.cekOngkir(),
            child: Text(
              "Cek Ongkos Kirim",
              style: TextStyle(fontSize: 18),
            ),
            style: ElevatedButton.styleFrom(
              backgroundColor: Colors.green[600],
              foregroundColor: Colors.white,
              shape: RoundedRectangleBorder(
                borderRadius: BorderRadius.circular(5),
              ),
            ),
          )
        ],
      ),
    );
  }
}

```

### 11. Code untuk Controller nya.
```dart
import 'package:dio/dio.dart';
import 'package:flutter/material.dart';
import 'package:get/get.dart';
import 'package:ongkir/app/data/models/ongkir_model.dart';

class HomeController extends GetxController {
  TextEditingController beratC = TextEditingController();

  RxInt provinsiAsalId = 0.obs;
  RxInt kotaAsalId = 0.obs;

  RxInt provinsiTujuanAsalId = 0.obs;
  RxInt kotaTujuanAsalId = 0.obs;

  RxString kurirId = ''.obs;

  List<Ongkir> ongkosKirim = [];

  void cekOngkir() async {
    if (provinsiAsalId.value != 0 &&
        provinsiTujuanAsalId.value != 0 &&
        kotaAsalId.value != 0 &&
        kotaTujuanAsalId.value != 0 &&
        kurirId.value.isNotEmpty &&
        beratC.text.isNotEmpty) {
      try {
        var response = await Dio().post(
          "https://api.rajaongkir.com/starter/cost",
          data: {
            "origin": kotaAsalId.value.toString(),
            "destination": kotaTujuanAsalId.value.toString(),
            "weight": int.parse(beratC.text),
            "courier": kurirId.value,
          },
          options: Options(
            headers: {
              "key": "59437d1d50e23a94d13e440f8ad72cb1",
            },
          ),
        );
        var hasil = response.data['rajaongkir']['results'][0]['costs'];

        ongkosKirim = List<Ongkir>.from(
          hasil.map(
            (item) => Ongkir.fromJson(item),
          ),
        );
        // for (var ongkir in ongkosKirim) {
        //   print('Service: ${ongkir.service}');
        //   print('Description: ${ongkir.description}');
        //   for (var cost in ongkir.cost!) {
        //     print('Cost: ${cost.value}');
        //     print('ETD: ${cost.etd}');
        //     print('Note: ${cost.note}');
        //   }
        // }

        Get.defaultDialog(
          title: "Ongkir",
          content: Column(
            mainAxisAlignment: MainAxisAlignment.start,
            children: ongkosKirim.map((ongkir) {
              return Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: [
                  Text(
                    'Type: ${ongkir.service ?? 'Unknown'}',
                    style: TextStyle(fontWeight: FontWeight.bold),
                  ),
                  Column(
                    children: ongkir.cost!.map((cost) {
                      return ListTile(
                        title: Text('Harga: ${cost.value ?? 'Unknown'}'),
                        subtitle: Text(
                            'Estimasi: ${cost.etd ?? 'Unknown'}\nNote: ${cost.note ?? 'No Note'}'),
                      );
                    }).toList(),
                  ),
                ],
              );
            }).toList(),
          ),
        );
      } catch (e) {
        if (e is DioException) {
          print(e.response?.data);
          Get.defaultDialog(
            title: "System",
            middleText: "Error: ${e.response?.data ?? e.message}",
            backgroundColor: Colors.green[200],
          );
        } else {
          Get.defaultDialog(
            title: "System",
            middleText: "Unknown Error: ${e.toString()}",
            backgroundColor: Colors.green[200],
          );
        }
      }
    } else {
      Get.defaultDialog(
        title: "System",
        middleText: "Terjadi Kesalahan: Semua field harus diisi.",
        backgroundColor: Colors.green[200],
      );
    }
  }
}

```
