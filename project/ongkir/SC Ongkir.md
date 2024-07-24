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
