---
title: Kontenerisasi App dengan Docker
date: 2024-11-28
categories: [Development]
tags: [Docker, DevOps, Linux]
---

## Apa itu Kontainer?
Kontainer adalah unit perangkat lunak yang memungkinkan pengembang untuk mengemas aplikasi dan semua dependensinya ke dalam satu paket. Kontainer memungkinkan aplikasi untuk berjalan di lingkungan yang terisolasi. Kontainer juga memungkinkan pengembang untuk memastikan aplikasi berjalan dengan benar di lingkungan yang berbeda.

## Bagaimana Docker Bekerja?

{{<mermaid>}}

sequenceDiagram
    participant User
    participant Docker
    User->>Docker: Build image
    Docker->>Docker: Build container
    Docker->>User: Run container
    User->>Docker: Stop container
    Docker->>Docker: Remove container
    Docker->>User: Done

{{</mermaid>}}

Pada diagram di atas, kita dapat melihat bagaimana Docker bekerja. Pengguna membangun dengan perintah `docker build`. kemudian digunakan untuk membuat kontainer dengan perintah `docker run`. Ketika kontainer selesai berjalan, pengguna dapat menghentikan kontainer dengan perintah `docker stop` dan menghapusnya dengan perintah `docker rm`.

## Studi Kasus

Misalnya, pada kasus ini kita akan membuat kontainer dalam konteks CTF yang rentan terhadap `Shellshock` CVE-2014-6271.

```dockerfile
#file dockerfile
FROM ubuntu:14.04

# Install Bash yang rentan CVE-2014-6271
RUN apt-get update && \
    apt-get install -y bash=4.3-7ubuntu1 && \
    apt-get clean

# Tambahkan CGI sederhana
RUN mkdir -p /var/www/cgi-bin
COPY test.sh /var/www/cgi-bin/test.sh
RUN chmod +x /var/www/cgi-bin/test.sh

# Install Apache2 dan enable CGI
RUN apt-get install -y apache2 && \
    a2enmod cgi

# Konfigurasi Apache
RUN echo "ScriptAlias /cgi-bin/ /var/www/cgi-bin/" >> /etc/apache2/sites-enabled/000-default.conf

# Expose port untuk akses
EXPOSE 80

# Jalankan Apache di foreground
CMD ["apachectl", "-D", "FOREGROUND"]
```
1. `FROM` mendefinisikan image dasar yang akan digunakan untuk membangun image baru.
2. `RUN` menjalankan perintah di dalam kontainer.   
3. `COPY` menyalin file dari host ke dalam kontainer.
4. `EXPOSE` mengekspos port yang digunakan oleh kontainer.
5. `CMD` menjalankan perintah ketika kontainer dimulai.

```bash
#file test.sh
#!/bin/bash
echo "Hello World"
```
Setelah membuat Dockerfile di atas, kita dapat membangunnya dengan perintah 
```bash
$ docker build -t shellshock .
```
Langkah selanjutnya adalah menjalankan kontainer dengan perintah
```bash
$ docker run -d -p 8080:80 shellshock
```
{{<alert>}}

**Catatan**: Untuk pengujian, pastikan Anda menjalankan kontainer ini di lingkungan yang terisolasi karena rentan terhadap serangan `Shellshock`.

{{</alert>}}

dan kita dapat mengaksesnya melalui `http://localhost:8080/cgi-bin/test.sh`.

## Akses Kontainer

Untuk mengakses kontainer, kita dapat menggunakan perintah `docker exec`. Misalnya, untuk masuk ke dalam kontainer, kita dapat menggunakan perintah berikut:
```bash
$ docker exec -it <container_id> /bin/bash
```

### Start, Stop, dan Remove Kontainer

Untuk memulai kontainer, gunakan perintah 
```bash
$ docker start <container_id>
```
Untuk menghentikan kontainer, gunakan perintah 
```bash
$ docker stop <container_id>
```
Untuk menghapus kontainer, gunakan perintah 
```bash
$ docker rm <container_id>
```

### Menghapus Images

Untuk menghapus image, gunakan perintah
```bash
$ docker rmi <image_id>
```

Dengan demikian, kita telah melihat bagaimana kontainerisasi bekerja dengan Docker dan bagaimana kita dapat membuat kontainer tertentu untuk keperluan pengujian.