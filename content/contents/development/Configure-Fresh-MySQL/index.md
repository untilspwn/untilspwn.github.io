---
title: Configure Fresh MySQL Server Install on Ubuntu
date: 2024-08-24
categories: [Web Development]
tags: [MySQL, Linux]
---

MySQL adalah database server yang populer digunakan untuk menyimpan data.
Pada artikel ini, saya akan menunjukkan cara mengkonfigurasi MySQL server yang baru diinstal pada Ubuntu.

## Langkah 1: Instal MySQL Server
```bash
sudo apt update
sudo apt install mysql-server
```

## Langkah 2: Konfigurasi MySQL Server
```bash
sudo mysql_secure_installation
```

Sekarang MySQL server sudah terkonfigurasi dan siap dihubungkan melalui port `3306`.

## Masalah yang sering terjadi saat mengkonfigurasi MySQL Server pertama kali
beberapa masalah yang sering terjadi saat mengkonfigurasi MySQL Server pertama kali adalah:
biasanya saat mengkonfigurasi MySQL Server pertama kali, secara default MySQL mengatur password root MySQL, `user=root, password=empty`. Jika Mencoba login menggunakan password kosong, akan muncul pesan error.

{{< alert >}}
`ERROR 1698 (28000): Access denied for user 'root'@'localhost'`
{{< /alert >}}

Untuk mengatasi masalah ini, bisa mengikuti langkah berikut:

1. Start MySQL dengan `sudo`.
```bash
sudo mysql
```

2. Reset password root MySQL
```sql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'New_Password';
FLUSH PRIVILEGES;
EXIT;
```
3. Restart MySQL dan login dengan password baru
```bash
sudo systemctl restart mysql
mysql -u root -p
```
    
{{< alert >}}
**Catatan**: untuk versi MySQL Terbaru seperti 8.0 keatas, tidak bisa login menggunakan perintah `mysql -u root -p new_password`, Anda harus login menggunakan perintah `mysql -u root -p` kemudian masukkan password.
{{< /alert >}}

Mungkin itu saja yang bisa saya bagikan tentang cara mengkonfigurasi MySQL Server yang baru diinstal pada Ubuntu. Jika masih ada error diluar pembahasan diatas, bisa bertanya lewat ChatGPT atau pakai Google. Semoga bermanfaat.