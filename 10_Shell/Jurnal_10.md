# Modul X - Shell dan Modifikasi System Call Xinu

## Identitas

**Nama** : Ardhian Dwi Saputra
**NIM** : 2311104040
**Mata Kuliah** : Sistem Operasi
**Modul** : Modul X - Shell

---

## Deskripsi

Praktikum ini bertujuan untuk memahami mekanisme kerja shell pada sistem operasi Xinu serta melakukan modifikasi kernel dengan menambahkan system call baru bernama `chname()`. Selain itu, dibuat command shell baru bernama `namecmd` yang berfungsi untuk memanggil system call tersebut sehingga pengguna dapat mengubah nama suatu proses melalui shell.

---

## Tujuan Praktikum

1. Memahami mekanisme kerja shell pada sistem operasi Xinu.
2. Memahami proses penambahan command baru pada shell.
3. Memahami implementasi dan penggunaan system call.
4. Membuat system call baru `chname()`.
5. Mengintegrasikan command shell dengan system call yang dibuat.

---

## Implementasi

### 1. Menambahkan System Call `chname()`

System call `chname()` dibuat untuk mengubah nama proses berdasarkan Process ID (PID) yang diberikan.

Prototype fungsi ditambahkan pada:

```c
include/prototypes.h
```

```c
extern syscall chname(pid32, char *, uint32);
```

Implementasi fungsi dibuat pada:

```c
system/chname.c
```

---

### 2. Menambahkan Command Shell `namecmd`

Command shell baru ditambahkan dengan nama:

```text
namecmd
```

Implementasi command berada pada file:

```c
shell/xsh_namecmd.c
```

Perintah ini digunakan untuk memanggil system call `chname()` dan menampilkan informasi yang diberikan pengguna.

---

### 3. Registrasi Command

Agar command dapat dikenali oleh shell, perlu ditambahkan ke tabel command pada:

```c
shell/shell.c
```

Contoh:

```c
{"namecmd", xsh_namecmd},
```

---

## Cara Kompilasi

Masuk ke direktori compile:

```bash
cd ~/xinu/compile
```

Kemudian jalankan:

```bash
make
```

Jika proses kompilasi berhasil, file image Xinu akan diperbarui secara otomatis.

---

## Menjalankan Xinu

Jalankan backend terlebih dahulu kemudian buka serial console menggunakan:

```bash
sudo minicom
```

Jika berhasil, akan muncul tampilan:

```text
Welcome to Xinu!
xsh $
```

---

## Pengujian

Melihat daftar proses:

```text
xsh $ ps
```

Menjalankan command baru:

```text
xsh $ namecmd Ardhian_Dwi_Saputra 2311104040
```

Contoh output:

```text
My new command
Argumen pertama adalah: Ardhian_Dwi_Saputra
Argumen kedua adalah: 2311104040
```

Melihat perubahan setelah pemanggilan system call:

```text
xsh $ ps
```

---

## Struktur File yang Dimodifikasi

```text
include/prototypes.h
system/chname.c
shell/xsh_namecmd.c
shell/shell.c
shell/shprototypes.h
```

---

## Hasil

System call `chname()` berhasil ditambahkan ke dalam kernel Xinu dan command shell `namecmd` berhasil dibuat serta dapat dijalankan melalui shell. Integrasi antara shell dan kernel berhasil dilakukan sehingga command baru dapat memanfaatkan layanan system call yang telah dibuat.

![Hasil Pengujian Namecmd](hasil.png)
---

## Kesimpulan

Melalui praktikum ini telah dipelajari cara kerja shell pada sistem operasi Xinu, proses penambahan command baru, serta implementasi system call pada kernel. Hasil praktikum menunjukkan bahwa shell dapat diperluas dengan menambahkan command baru dan diintegrasikan dengan system call untuk menyediakan layanan tambahan kepada pengguna.
