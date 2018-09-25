# Learn Git

### 1. Membuat repository

```sh
$ cd existing_folder
$ git init
$ git remote add origin "ssh/https"
$ git add .
$ git commit m "Initial commit"
$ git push u origin master
```

| Kode | Penjelasan |
| ------ | ------ |
| cd existing_folder | Menuju ke direktori tertentu |
| git init | Memulai Repository di Direktori Tersedia |
| git remote add origin "ssh/https" | Mengatur atau menambahkan lokasi remote |
| git add . | Memasukkan semua perubahan atau file ke stage |
| git commit m "Initial commit" | Membuat commit dan menambahkan pesan |
| git push u origin master | Mengirim perubahan ke server git |