---
title: Linux Privilage
date: 2024-10-27
categories: [Development, DevOps]
tags: [Linux, System]
---

# Linux Privilage


## chmod
`chmod` perintah di sistem operasi Unix/Linux yang digunakan untuk mengubah izin (permissions) dari file atau direktori.

### Sintaks

```bash
chmod [options] mode file
```
- `options` : opsi yang dapat digunakan.
- `mode` : mode yang akan diberikan pada file atau direktori.
- `file` : file atau direktori yang akan diberikan mode.

**mode numerik**

Numerik mode(octal number) :
- `0` : tidak ada izin
- `1` : eksekusi
- `2` : tulis
- `4` : baca

{{<alert>}}
(4+2+1) = 7. Maka, 7 = read + write + execute (rwx)
{{</alert>}}

**mode simbolik**
Simbolik mode :
- `u` : pemilik file
- `g` : grup file
- `o` : lainnya
- `a` : semua
- `+` : menambahkan hak akses
- `-` : menghapus hak akses
- `=` : mengganti hak akses
{{<alert>}}
contoh : `u+rwx` = menambahkan hak akses `read`, `write`, dan `execute` pada pemilik file.
{{</alert>}}

### Penggunaan chmod Mode Numerik
```bash
chmod 775 file.txt
```
maka, file.txt akan memiliki izin seperti berikut :
```bash
-rwxrwxr-x  1 dilz ubuntu   22 Oct 27 20:01 file.txt
```

### Penggunaan chmod Mode Simbolik
```bash
chmod u+rwx,g+rx,o+r file.txt
```
maka, file.txt akan memiliki izin seperti berikut :
```bash
-rwxr-xr--  1 dilz ubuntu   22 Oct 27 20:01 file.txt
```

Perhatikan bahwa ada 3 grup izin yang diberikan pada file.txt
- `rwx` : pemilik file
- `r-x` : grup file
- `r--` : lainnya

```bash
-rwx|rwx|r-x
^ ^   ^   ^
| |   |   |
t u   g   o
```

- `t` : tipe
- `u` : pemilik file
- `g` : grup file
- `o` : lainnya

## chown

`chown` perintah di sistem operasi Unix/Linux yang digunakan untuk mengubah kepemilikan file atau direktori.

### Sintaks

```bash
chown [options] user:group file
```

- `options` : opsi yang dapat digunakan.
- `user` : nama pengguna yang akan diberikan kepemilikan.
- `group` : nama grup yang akan diberikan kepemilikan.
- `file` : file atau direktori yang akan diberikan kepemilikan.

### Penggunaan chown
```bash
chown cecep:ubuntu file.txt
```

maka, file.txt akan memiliki kepemilikan seperti berikut :
```bash
-rwxrwxr-x  1 cecep ubuntu   22 Oct 27 20:01 file.txt
```

Selain itu, kita juga dapat menggunakan opsi `-R` untuk mengubah kepemilikan secara rekursif pada direktori dan subdirektori.

## Tips penggunaan chmod dan chown
- Jangan memberikan hak akses yang tidak perlu pada file atau direktori.
- Jangan memberikan hak akses `777` pada file atau direktori.
- Jangan memberikan kepemilikan file atau direktori pada pengguna yang tidak perlu.
- Gunakan opsi `-R` dengan hati-hati, karena dapat merubah kepemilikan secara rekursif pada direktori dan subdirektori.
