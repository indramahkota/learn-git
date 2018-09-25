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

### 5. Mengubah Commit Terakhir Anda

#### Intro Sebagai Peringatan agar Berhati-Hati dalam Menggunakan Perintah Ini.
Pada setiap tahapan, Anda mungkin ingin membatalkan sesuatu. Di sini, kita akan membahas beberapa alat dasar untuk membatalkan perubahan yang baru saja Anda lakukan. Harus tetap diingat bahwa kita tidak selalu dapat membatalkan apa yang telah kita batalkan. Ini adalah salah satu area dalam Git yang dapat membuat Anda kehilangan apa yang telah Anda kerjakan jika Anda melakukannya dengan tidak tepat.

#### Jika Commit Belum di Push

```sh
$ git commit --amend //Peringatan!!! Jangan gunakan perintah ini secara langsung.
```

Ketika selesai melakukan perubahan pada file dan menggunakan perintah ``$ git commit -m 'Pesan Commit'`` untuk commit, secara tidak sengaja Anda lupa mengubah atau menambahkan ``add <file>..`` file. Anda dapat mengubah commit terakhir tersebut dengan cara sebagai berikut:

```sh
$ git commit -m 'Pesan Commit'
$ git add forgotten_file
$ git commit -m 'Pesan Commit' --amend
```

Peringatan!!! Perintah diatas Harus digunakan secara lengkap karena jika tidak lengkap misal tidak menuliskan ``-m "Pesan Commit"`` perintah ini akan membuka teks editor di cmd/powershell/gitbash yang saya sendiri tidak paham cara menggunakannya, jika Anda bypass atau melewati tahap ini dengan cara menutup cmd/powershell/gitbash maka akan muncul pesan error pada perintah git yang akan Anda tulis berikutnya.

```sh
Another git process seems to be running in this repository, e.g.
an editor opened by 'git commit'. Please make sure all processes
are terminated then try again. If it still fails, a git process
may have crashed in this repository earlier:
remove the file manually to continue.
```

Untuk mengatasi ini, caranya masuk ke direktori .git pada repository dan hapus file index.lock.

#### Jika Commit Sudah di Push

Jika commit sudah terlanjur di push ke server git, sebenarnya jangan terlalu khawatir. Langkah-langkah mengembalikan atau mengubah commit terakhir tersebut dijelaskan sebagai berikut. Ini hanya cara saya, saya menganggap cara ini yang paling baik atau satu-satunya untuk mengatasi masalah ini. Pertama simpan perubahan file terakhir Anda yang sudah di push tadi ke dalam file yang baru katakan saja ``file_baru.txt``, lalu gunakan perintah dibawah ini untuk menghapus commit terakhir Anda yang telah di push.

```sh
$ git reset HEAD^ --hard
```

Lalu setelah Anda menjalankan perintah diatas, gunakan perintah dibawah ini untuk membatalkan commit yang telah Anda push di server git.

```sh
$ git push origin -f
```

Khusus untuk gitlab, jika commit yang akan dibatalkan berada di cabang master, maka harus ada pengaturan konfigurasi yang diubah pada website gitlab karena secara default, cabang master di proteksi oleh gitlab untuk mencegah penyalahgunaan atau pelanggaran pengembangan secara berkelompok. Pengaturan tersebut terletak pada halaman``settings/repository`` khususnya di ``Protected Branches`` tekan tombol Expand dan tekan tombol ``Unprotect`` pada cabang master yang diproteksi.

Setelah menjalankan perintah diatas, buat ulang perubahan yang Anda inginkan untuk commit dan push kembali ke server git.

### 6. Menandai

Git memiliki kemampuan untuk menandai titik tertentu dalam (history atau commit-commit yang Anda buat) sebagai sesuatu yang penting. Biasanya, orang menggunakan fungsi ini untuk menandai titik-titik release (rilis) (v1.0, dan seterusnya). Untuk membuat tanda yang diinginkan pada titik commit tertentu gunakan perintah dibawah ini:

```sh
$ git tag v1.0
```

Untuk memberikan tanda dan pesan terhadap tanda tersebut, gunakan perintah dibawah ini:

```sh
$ git tag -a v1.0 -m 'Version 1.0'
```

Untuk melihat data pada tanda yang telah dibuat dapat menggunakan perintah sebagai berikut:

```sh
$ git show v1.0
```

Hasil:

```sh
$ git show v1.0
commit a2513c953def4339b4934952352a31472d634b97 (HEAD -> master, tag: v1.0, origin/master)
Author: Indra Mahkota <indramahkota1@gmail.com>
Date:   Tue Sep 25 22:59:22 2018 +0700

    Mengubah Commit Terakhir Anda

diff --git a/ReadMe.md b/ReadMe.md
index 7ea371e..3349833 100644
--- a/ReadMe.md
+++ b/ReadMe.md
@@ -88,4 +88,51 @@ Untuk membatalkan semua perubahan pada file tertentu sehingga mengembalikannya s

 ```sh
 $ git checkout -- <file>
-```
\ No newline at end of file
+```
+
+### 5. Mengubah Commit Terakhir Anda
+
+#### Intro Sebagai Peringatan agar Berhati-Hati dalam Menggunakan Perintah Ini.
+Pada setiap tahapan, Anda mungkin ingin membatalkan sesuatu. Di sini, kita akan membahas beberapa alat dasar untuk membatalkan perubahan yang baru saja Anda lakukan. Harus tetap diingat bahwa kita tidak selalu dapat membatalkan apa yang telah kita batalkan. Ini adalah salah satu area dalam Git yang dapat membuat Anda kehilangan apa yang telah Anda kerjakan jika Anda melakukannya dengan tidak tepat.
+
+#### Jika Commit Belum di Push
+
+```sh
+$ git commit --amend //Peringatan!!! Jangan gunakan perintah ini secara langsung.
+```
+
+Ketika selesai melakukan perubahan pada file dan menggunakan perintah ``$ git commit -m 'Pesan Commit'`` untuk commit, secara tidak sengaja Anda lupa mengubah atau menambahkan ``add <file>..`` file. Anda dapat mengubah commit terakhir tersebut dengan cara sebagai berikut:
+
+```sh
+$ git commit -m 'Pesan Commit'
+$ git add forgotten_file
+$ git commit -m 'Pesan Commit' --amend
+```
+
+Peringatan!!! Perintah diatas Harus digunakan secara lengkap karena jika tidak lengkap misal tidak menuliskan ``-m "Pesan Commit"`` perintah ini akan membuka teks editor di cmd/powershell/gitbash yang saya sendiri tidak paham cara menggunakannya, jika Anda bypass atau melewati tahap ini dengan cara menutup cmd/powershell/gitbash maka akan muncul pesan error pada perintah git yang akan Anda tulis berikutnya.
+
+```sh
+Another git process seems to be running in this repository, e.g.
+an editor opened by 'git commit'. Please make sure all processes
+are terminated then try again. If it still fails, a git process
+may have crashed in this repository earlier:
+remove the file manually to continue.
+```
+
+Untuk mengatasi ini, caranya masuk ke direktori .git pada repository dan hapus file index.lock.
+
+#### Jika Commit Sudah di Push
+
+Jika commit sudah terlanjur di push ke server git, sebenarnya jangan terlalu khawatir. Langkah-langkah mengembalikan atau mengubah commit terakhir tersebut dijelaskan sebagai berikut. Ini hanya cara saya, saya menganggap cara ini yang paling baik atau satu-satunya untuk mengatasi masalah ini. Pertama simpan perubahan file terakhir Anda yang sudah di push tadi ke dalam file yang baru katakan saja ``file_baru.txt``, lalu gunakan perintah dibawah ini untuk menghapus commit terakhir Anda yang telah di push.
+
+```sh
+$ git reset HEAD^ --hard
+```
+
+Lalu setelah Anda menjalankan perintah diatas, gunakan perintah dibawah ini untuk membatalkan commit yang telah Anda push di server git.
+
+```sh
+$ git push origin -f
+```
+
+Setelah menjalankan perintah diatas, buat ulang perubahan yang Anda inginkan untuk commit dan push kembali ke server git.
\ No newline at end of file
(END)
```