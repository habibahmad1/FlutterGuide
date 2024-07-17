# GetX CLI Install Flutter
### 1. Download GetX CLI dengan Command ini.
```dart
flutter pub global activate --source=git https://github.com/inyong1/get_cli.git"
```

### 2. Setelah selesai download maka daftarkan ke Environment Variabel Path nya.
```dart
C:/Users/asus/AppData/Local/Pub/Cache/bin
```

### 3. Cek apakah sudah bisa dicek berhasil install.
```dart
/c/Users/asus/AppData/Local/Pub/Cache/bin/get.bat --version
```

### 4. Buat file untuk menyimpan alias yang akan digunakan.
```dart
nano ~/.bashrc
```

### 5. Buat Alias didalam file bashrc itu agar path tersimpan terus dan mudah di gunakan Command nya. Setelah ketik itu lalu tekan CTRL+O lalu Enter untuk simpan file baru.
```dart
alias get='/c/Users/asus/AppData/Local/Pub/Cache/bin/get.bat'
```

### 6. Simpan agar bisa otomatis digunakan alias nya ketika buka terminal baru tanpa alias ulang.
```dart
source ~/.bashrc
```

### 7. Cek lagi apakah sudah berhasil di install dengan ketik
```dart
get --version
```

