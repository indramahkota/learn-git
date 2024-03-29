# Learn Git

## Learn how git works

### 0. Memulai Git

* Download Git Bash.
* Install Git Bash.
* Masukkan username.

```sh
git config --global user.name "indramahkota"
```

* Masukkan email.

```sh
git config --global user.email myemail@gmail.com
```

* Membuat ssh.

```sh
ssh-keygen
```

* Upload ssh.

### 1. Membuat repository

```sh
cd existing_folder
git init
git remote add origin "ssh/https"
git add .
git commit m "Initial commit"
git push u origin master
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
git clone git@gitlab.com:indramahkota/learngit.git
```

```sh
git clone -b nama-branch git@gitlab.com:indramahkota/learngit.git
```

#### Penjelasan #2

* Ambil link berupa "ssh/https" pada repository.
* Tentukan lokasi penyimpanan di komputer Anda.
* Block lokasi yang ada pada menu bar komputer Anda.
* Tulis cmd pada lokasi, lalu tekan Enter.
* Jalankan perintah pada cmd sesuai dengan contoh diatas.
* Jalankan perintah kedua untuk mengclone spesifik branch.

### 3. Cek Status dari Berkas Anda

```sh
git status
```

#### Hasil

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

#### Penjelasan #3

* git status akan menampilkan status file-file pada project Anda.
* git add ``<file>...`` untuk menambahkan semua ``<file>...`` yang telah diubah kedalam stage.
* git checkout -- ``<file>...`` untuk membatalkan perubahan semua ``<file>...`` sehingga mengembalikannya seperti semula pada saat commit sebelumnya.

### 4. Melewatkan Perintah add Sebelum Commit

```sh
git commit -a -m 'added new benchmarks'
```

```sh
git commit -am 'added new benchmarks'
```

#### Penjelasan #4

Dengan memberikan opsi ``-a`` ke perintah ``git commit``, akan membuat Git secara otomatis menempatkan setiap berkas yang telah terpantau sebelumnya ke area stage. Hal itu akan mempermudah Anda karena menskip 1 langkah yaitu ``git add``.

### 5. Menghapus Berkas dari Stage

Untuk menghapus file dari pantauan atau stage gunakan perintah reset HEAD dimana HEAD adalah commit terakhir branch saat ini. Contoh: Anda membuat file ``.gitignore``, lalu Anda gunakan perintah ``$ git add .gitignore``, file ``.gitignore`` akan masuk pada pantauan atau stage, lalu Anda gunakan perintah ``$ git reset HEAD .gitignore`` maka file .gitignore akan keluar dari pantauan atau stage. Perubahan yang telah dilakukan tidak akan hilang.

```sh
git reset HEAD <file>
```

Hampir sama dengan perintah diatas, perintah ``git rm file.js --cache`` akan menghapus file dari pantauan atau stage setelah ditambahkan dengan perintah ``$ git add <file>``. Untuk menghentikan pemantauan file sehingga keluar dari repository tetapi masih tetap berada pada disk direktori komputer Anda. Untuk mencegah file dipantau dimasa mendatang, masukkan file yang akan Anda hentikan pemantauannya ke dalam file .gitignore.

```sh
git rm file.js --cache
```

Untuk membatalkan semua perubahan pada file tertentu sehingga mengembalikannya seperti semula pada saat commit sebelumnya gunakan perintah. //Peringatan!!! Hati-hati menggunakan perintah ini.

```sh
git checkout -- <file>
```

### 6. Mengubah Commit Terakhir Anda

#### Intro Sebagai Peringatan agar Berhati-Hati dalam Menggunakan Perintah Ini

Pada setiap tahapan, Anda mungkin ingin membatalkan sesuatu. Di sini, kita akan membahas beberapa perintah dasar untuk membatalkan perubahan yang baru saja dilakukan. Harus tetap diingat bahwa kita tidak selalu dapat membatalkan apa yang telah kita kerjakan. Ini adalah salah satu area dalam Git yang dapat membuat Anda kehilangan apa yang telah Anda kerjakan jika Anda melakukannya dengan tidak tepat.

#### Jika Commit Belum di Push

```sh
git commit --amend //Peringatan!!! Jangan gunakan perintah ini secara langsung.
```

Ketika selesai melakukan perubahan pada file dan menggunakan perintah ``$ git commit -m 'Pesan Commit'`` untuk commit, secara tidak sengaja Anda lupa mengubah atau menambahkan ``add <file>..`` file. Anda dapat mengubah commit terakhir tersebut dengan cara sebagai berikut:

```sh
git commit -m 'Pesan Commit'
git add forgotten_file
git commit -m 'Pesan Commit' --amend
```

Peringatan!!! Perintah diatas Harus digunakan secara lengkap karena jika tidak lengkap misal tidak menuliskan ``-m "Pesan Commit"`` perintah ini akan membuka teks editor di cmd/powershell/gitbash, jika Anda bypass atau melewati tahap ini dengan cara menutup cmd/powershell/gitbash maka akan muncul pesan error pada perintah git yang akan Anda tulis berikutnya.

```sh
Another git process seems to be running in this repository, e.g.
an editor opened by 'git commit'. Please make sure all processes
are terminated then try again. If it still fails, a git process
may have crashed in this repository earlier:
remove the file manually to continue.
```

Untuk mengatasi ini, caranya masuk ke direktori .git pada repository dan hapus file index.lock.

#### Jika Commit Sudah di Push

Jika commit sudah terlanjur di push ke server git, sebenarnya jangan terlalu khawatir. Langkah-langkah mengembalikan atau mengubah commit terakhir tersebut dijelaskan sebagai berikut. Sebagai catatan, ini hanya cara sederhana saya sebagai pemula, saya menganggap cara ini cukup baik untuk mengatasi masalah ini. Pertama simpan perubahan file terakhir Anda yang sudah di push tadi ke dalam file yang baru katakan saja ``file_baru.txt``/ salin seluruh project/ simpan perubahan pada stash, lalu gunakan perintah dibawah ini untuk menghapus commit terakhir Anda yang telah di push.

```sh
git reset HEAD^ --hard
```

Lalu setelah Anda menjalankan perintah diatas, gunakan perintah dibawah ini untuk membatalkan commit yang telah Anda push di server git.

```sh
git push origin -f
```

#### Jika Commit Sudah di Push dan Hanya Ingin Mengubah Pesannya Saja

```sh
git commit -m 'Pesan Commit' --amend
git push origin -f
```

Khusus untuk gitlab, jika commit yang akan dibatalkan berada di cabang master, maka harus ada pengaturan konfigurasi yang diubah pada website gitlab karena secara default, cabang master di proteksi oleh gitlab untuk mencegah penyalahgunaan atau pelanggaran pengembangan secara berkelompok. Pengaturan tersebut terletak pada halaman``settings/repository`` khususnya di ``Protected Branches`` tekan tombol Expand dan tekan tombol ``Unprotect`` pada cabang master yang diproteksi.

Setelah menjalankan perintah diatas, buat ulang perubahan yang Anda inginkan untuk commit dan push kembali ke server git.

### 7. Menandai

Git memiliki kemampuan untuk menandai titik tertentu dalam (history atau commit-commit yang Anda buat) sebagai sesuatu yang penting. Biasanya, orang menggunakan fungsi ini untuk menandai titik-titik release (rilis) (v1.0, dan seterusnya). Untuk membuat tanda yang diinginkan pada titik commit tertentu gunakan perintah dibawah ini:

```sh
git tag v1.0
```

Untuk memberikan tanda dan pesan terhadap tanda tersebut, gunakan perintah dibawah ini:

```sh
git tag -a v1.0 -m 'Version 1.0'
```

Untuk melihat data pada tanda yang telah dibuat dapat menggunakan perintah sebagai berikut:

```sh
git show v1.0
```

Hasil:

```sh
$ git show v1.0
commit a2513c953def4339b4934952352a31472d634b97 (HEAD -> master, tag: v1.0, origin/master)
Author: Indra Mahkota <indramahkota1@gmail.com>
Date:   Tue Sep 25 22:59:22 2018 +0700
... details ...
```

### 8. Mengecek log dengan decoration

find source in [atlassian webpage](https://www.atlassian.com/git/tutorials/git-log)

```sh
git log -3
```

```sh
git log --after="2014-7-1"
```

```sh
git log --after="yesterday"
```

```sh
git log --after="2014-7-1" --before="2014-7-4"
```

```sh
git log --author="John"
```

```sh
git log --author="John\|Mary"
```

```sh
git log --grep="JRA-224:"
```

```sh
git log --graph --oneline --decorate
```

```sh
git log --pretty=format:"%cn committed %h on %cd"
```

```sh
git log --all --graph --decorate --oneline --simplify-by-decoration
```

### 9. Menghapus semua commit history serta menyisakan current state code

```sh
git checkout --orphan latest_branch
git add -A
git commit -am "Initial commit"
git branch -D master
git branch -m master
git push -f origin master
```

#### Penjelasan #9

| Kode | Penjelasan |
| ------ | ------ |
| git checkout --orphan latest_branch | Membuat branch baru di state saat ini dan tidak memasukkan commit history |
| git add -A | Memasukkan semua perubahan dan file baru kedalam stage |
| git commit -am "Initial commit" | Membuat pesan commit |
| git branch -D master | Menghapus branch master |
| git branch -m master | Mengubah nama branch saat ini menjadi master |
| git push -f origin master | Mengirim perubahan ke server git secara paksa |

### 10. Website penjelasan script shell

find source in [ExplainShell](https://explainshell.com)
