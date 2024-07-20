# GetX Model Flutter
1. Buat dahulu project kosong pada flutter.
```dart
  flutter create project_latihant
```

2. Lalu setelah dibuat maka tinggal buat menjadi Pattern GetX dengan ketik ini.
```dart
get init
```

3. Setelah itu Buat folder pada root dengan assets lalu buat lagi folder dengan nama models dan di isi dengan file misal user.json dan isinya seperti ini.
```dart
{
  "id": 7,
  "email": "michael.lawson@reqres.in",
  "first_name": "Michael",
  "last_name": "Lawson",
  "avatar": "https://reqres.in/img/faces/7-image.jpg"
}

```

4. Setelah itu buat model agar bisa dibuatkan di folder app dengan ketik.
```dart
get generate model with assets/models/user.json
```

5. 
