---
title: OSI Layer Model
date: 2024-10-07
categories: [Cyber Security]
tags: [OSI, Model]
---

# OSI Layer Model

Model OSI (Open Systems Interconnection) adalah model referensi yang menggambarkan bagaimana aplikasi dapat berkomunikasi dengan perangkat lainnya. Model ini terdiri dari tujuh lapisan, dan setiap lapisan memiliki fungsi tertentu. Model ini memungkinkan berbagai perangkat keras dan perangkat lunak untuk berkomunikasi dengan mudah.

## Lapisan OSI

{{< mermaid >}}
graph TD;
    A[Application Layer] --> B[Presentation Layer];
    B --> C[Session Layer];
    C --> D[Transport Layer];
    D --> E[Network Layer];
    E --> F[Data Link Layer];
    F --> G[Physical Layer];
{{< /mermaid >}}

1. **Physical Layer** (Lapisan Fisik): Bertanggung jawab untuk transmisi fisik bit antar perangkat. Menentukan bagaimana sinyal dikirim melalui media komunikasi.

2. **Data Link Layer** (Lapisan Tautan Data): Mengirimkan frame antar perangkat di jaringan lokal, sekaligus menangani koreksi kesalahan yang terjadi pada lapisan fisik.

3. **Network Layer** (Lapisan Jaringan): Mengatur pengiriman paket data antar jaringan serta menentukan jalur terbaik (routing) yang diambil oleh paket.

4. **Transport Layer** (Lapisan Transport): Menyediakan pengiriman data yang andal antar perangkat, termasuk kontrol kesalahan yang terjadi pada lapisan jaringan.

5. **Session Layer** (Lapisan Sesi): Mengatur, memelihara, dan mengelola sesi komunikasi antara aplikasi yang berjalan di dua perangkat.

6. **Presentation Layer** (Lapisan Presentasi): Bertanggung jawab untuk mengonversi data antara format yang digunakan oleh aplikasi dan format yang dibutuhkan untuk transmisi.

7. **Application Layer** (Lapisan Aplikasi): Menyediakan layanan jaringan langsung kepada pengguna, seperti email, browsing web, atau transfer file.


## Celah Keamanan pada Setiap Lapisan OSI

1. **Physical Layer (Lapisan Fisik)**  
   **Celah**: 
   - Penyadapan fisik (wiretapping) atau intersepsi data pada media komunikasi.
   - Jamming atau gangguan sinyal pada perangkat nirkabel.
   - Serangan fisik pada perangkat jaringan (misalnya router, switch).

2. **Data Link Layer (Lapisan Tautan Data)**  
   **Celah**: 
   - *MAC Spoofing*: Penyerang menyamar sebagai perangkat dengan alamat MAC palsu untuk mengakses jaringan.
   - *ARP Spoofing*: Manipulasi tabel ARP untuk mengarahkan lalu lintas ke perangkat penyerang.
   - Serangan *VLAN hopping*: Menyusup ke VLAN lain yang seharusnya terisolasi.

3. **Network Layer (Lapisan Jaringan)**  
   **Celah**: 
   - *IP Spoofing*: Penyerang menyamar sebagai alamat IP lain untuk mengelabui target.
   - *Routing Attacks*: Manipulasi protokol routing untuk mengubah jalur data, seperti serangan *BGP hijacking*.
   - Serangan DDoS (Distributed Denial of Service) melalui banjir paket IP.

4. **Transport Layer (Lapisan Transportasi)**  
   **Celah**: 
   - *Port Scanning*: Mendeteksi port terbuka untuk eksploitasi lebih lanjut.
   - *TCP SYN Flood*: Membanjiri server dengan permintaan koneksi TCP untuk membuatnya tidak dapat melayani permintaan sah.
   - *Session Hijacking*: Penyerang mengambil alih sesi komunikasi dengan mencuri ID sesi.

5. **Session Layer (Lapisan Sesi)**  
   **Celah**: 
   - *Session Fixation*: Penyerang mengarahkan pengguna ke sesi yang telah ditentukan sebelumnya dan mengambil alih.
   - *Session Hijacking*: Pencurian sesi yang sah untuk menyusup ke komunikasi antara dua perangkat.

6. **Presentation Layer (Lapisan Presentasi)**  
   **Celah**: 
   - *Data Encryption Attacks*: Serangan terhadap enkripsi, seperti serangan *man-in-the-middle* (MITM) untuk mencuri atau mengubah data sebelum atau setelah enkripsi.
   - Serangan *code injection* jika data tidak diproses dengan benar.

7. **Application Layer (Lapisan Aplikasi)**  
   **Celah**: 
   - *Buffer Overflow*: Input yang terlalu besar dapat menyebabkan aplikasi crash atau dieksploitasi untuk menjalankan kode berbahaya.
   - *SQL Injection*: Menyisipkan perintah SQL ke dalam input aplikasi untuk mengakses atau memodifikasi basis data.
   - *Cross-Site Scripting (XSS)*: Menyuntikkan skrip berbahaya ke dalam aplikasi web untuk mencuri data pengguna.
