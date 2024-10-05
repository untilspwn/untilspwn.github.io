---
title: Configure PHPMyAdmin on Ubuntu
date: 2024-08-24
categories: [Web Development]
tags: [PHP, MySQL, PHPMyAdmin, Ubuntu]
---

PHPMyAdmin adalah aplikasi web yang digunakan untuk mengelola database MySQL. PHPMyAdmin memungkinkan pengguna untuk membuat, mengedit, dan menghapus database, tabel, dan field. PHPMyAdmin juga memungkinkan pengguna untuk menjalankan query SQL dan mengelola pengguna dan hak akses.

Pada artikel ini, saya akan menunjukkan cara mengkonfigurasi PHPMyAdmin pada Ubuntu. PHPMyAdmin membutuhkan web server dan PHP untuk berjalan. Oleh karena itu, pastikan Anda sudah menginstal web server dan PHP sebelum menginstal PHPMyAdmin.

## Langkah 1: Instal PHPMyAdmin
```bash
sudo apt update
sudo apt install phpmyadmin apache2 mysql-server php 
```
> **Catatan:** Saat Anda menjalankan perintah mungkin ada beberapa library yang dibutuhkan untuk menjalankan PHPMyAdmin.

## Langkah 2: Konfigurasi PHPMyAdmin
```bash
sudo phpenmod mbstring
sudo systemctl restart apache2

#tambah phpmyadmin ke apache2 www-data
sudo ln -s /usr/share/phpmyadmin /var/www/html/phpmyadmin
sudo systemctl restart apache2
```

## Beres!
Sekarang PHPMyAdmin sudah terkonfigurasi dan dapat mengakses PHPMyAdmin melalui browser dengan alamat `http://localhost/phpmyadmin`.