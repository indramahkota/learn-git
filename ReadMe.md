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

### 2. Duplikasi Repositori Tersedia

```sh
$ git clone git@gitlab.com:indramahkota/learngit.git
```

#### Penjelasan:
* Ambil link berupa "ssh/https" pada repository.
* Tentukan lokasi penyimpanan di komputer Anda.
* Block lokasi yang ada pada menu bar komputer Anda.
* Tulis cmd pada lokasi, lalu tekan Enter.
* Jalankan perintah pada cmd sesuai dengan contoh diatas.