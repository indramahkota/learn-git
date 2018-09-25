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

### 3. Cek Status dari Berkas Anda

```sh
$ git status
```

#### Hasil:

```sh
$ git status

On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   ReadMe.md

no changes added to commit (use "git add" and/or "git commit -a")
```

#### Penjelasan:
* $ git status akan menampilkan status file-file pada project Anda.
* $ git add ``<file>...`` untuk menambahkan semua ``<file>...`` yang telah diubah kedalam stage.
* $ git checkout -- ``<file>...`` untuk membatalkan perubahan semua ``<file>...`` sehingga mengembalikannya seperti semula pada saat commit sebelumnya.

### 3. Melewatkan Perintah add Sebelum Commit

```sh
$ git commit -a -m 'added new benchmarks'
```

#### Penjelasan:
Dengan memberikan opsi ``-a`` ke perintah ``git commit`` akan membuat Git secara otomatis menempatkan setiap berkas yang telah terpantau di area stage sebelum melakukan commit (khusus file yang sebelumnya telah di add dan mengalami perubahan), membuat Anda dapat melewatkan bagian ``git add``.

### 4. Menghapus Berkas dari Git

Untuk menghapus file dari pantauan atau stage gunakan perintah reset HEAD dimana HEAD adalah commit terakhir branch saat ini. Contoh: Anda membuat file ``.gitignore``, lalu Anda gunakan perintah ``$ git add .gitignore``, file ``.gitignore`` akan masuk pada pantauan atau stage, lalu Anda gunakan perintah ``$ git reset HEAD .gitignore`` maka file .gitignore akan keluar dari pantauan atau stage.

```sh
$ git reset HEAD <file>
```

Hampir sama dengan perintah diatas, perintah ``git rm file.js --cache`` akan menghapus file dari pantauan atau stage setelah ditambahkan dengan perintah ``$ git add <file>``. Untuk menghentikan pemantauan file sehingga keluar dari repository tetapi masih tetap berada pada disk atau komputer Anda, masukkan file yang akan Anda hentikan pemantauannya ke dalam file .gitignore.

```sh
git rm file.js --cache
```

Untuk membatalkan semua perubahan pada file tertentu sehingga mengembalikannya seperti semula pada saat commit sebelumnya gunakan perintah.

```sh
$ git checkout -- <file>
```