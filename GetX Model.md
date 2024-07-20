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

4. Setelah itu buat model agar bisa dibuatkan di folder app/data dengan ketik.
```dart
get generate model user with assets/models/user.json
```

5. Bertambah folder pada app ada folder baru yaitu models dan providers yang dibuatkan otomatis beserta isinya pada file yang ada di kedua folder tersebut.
6. Untuk file yang ada pada folder providers bisa kita sesuaikan dengan URL API kita.
```dart
import 'package:get/get.dart';
import '../models/user_model.dart';

class UserProvider extends GetConnect {
  Future<User?> getUser(int id) async {
    final response = await get('https://reqres.in/api/users/$id');
    if (response.status.hasError) {
      return Future.error(response.statusText ?? 'Error fetching user');
    } else {
      return User.fromJson(response.body['data']);
    }
  }

  Future<List<User>?> getAllUsers() async {
    final response = await get('https://reqres.in/api/users');
    if (response.status.hasError) {
      return Future.error(response.statusText ?? 'Error fetching users');
    } else {
      List<dynamic> data = response.body['data'];
      return data.map((userJson) => User.fromJson(userJson)).toList();
    }
  }
}

```

7. Lalu bisa langsung kita gunakan datanya di main code, jangan lupa di import User Model nya jika belum.
```dart
import 'package:flutter/material.dart';

import 'package:get/get.dart';

import '../controllers/home_controller.dart';

import '../../../data/models/user_model.dart';

class HomeView extends GetView<HomeController> {
  const HomeView({Key? key}) : super(key: key);
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('HomeView'),
        centerTitle: true,
      ),
      body: FutureBuilder<List<User>>(
          future: controller.getAllUsers(),
          builder: (context, snap) {
            if (snap.connectionState == ConnectionState.waiting) {
              return Center(
                child: CircularProgressIndicator(),
              );
            }

            if (snap.data?.length == 0) {
              return Center(
                child: Text("No Data"),
              );
            } else {
              return ListView.builder(
                itemCount: snap.data!.length,
                itemBuilder: (context, index) {
                  User user = snap.data![index];
                  return ListTile(
                    title: Text('${user.firstName} ${user.lastName}'),
                    leading: CircleAvatar(
                      backgroundImage: NetworkImage('${user.avatar}'),
                    ),
                    subtitle: Text('${user.email}'),
                  );
                },
              );
            }
          }),
    );
  }
}

```

8. Lalu pada controller home pada main code kita inisialisasikan ulang function pada model ke controller untuk singleUser dan allUsers.
```dart
UserProvider userProv = UserProvider();

  Future<User?> getSingleUser(int id) async {
    return await userProv.getUser(id);
  }

  Future<List<User>> getAllUsers() async {
    final users = await userProv.getAllUsers();
    return users ?? [];
  }
```

