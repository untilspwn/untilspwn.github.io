---
Title: Bagaimana cara SNI bekerja?
Date: 2024-10-09
---

# Bagaimana cara SNI bekerja?

*Server Name Indication* (SNI) adalah ekstensi protokol TLS yang memungkinkan klien untuk mengirimkan nama host tujuan sebagai bagian dari *TLS handshake*. Ini memungkinkan server untuk menggunakan sertifikat SSL/TLS yang berbeda pada satu alamat IP.

{{< mermaid >}}
sequenceDiagram
    participant Client
    participant Server
    participant TLS
    Client->>TLS: Client Hello (SNI in handshake)
    TLS->>Server: Server selection based on SNI
    Server->>TLS: Server Hello (with certificate)
    TLS->>Client: Server Certificate
    Client->>TLS: Finished (Encrypted handshake)
    TLS->>Server: Forward encrypted communication
    Server->>Client: Encrypted data
{{< /mermaid >}}

## Cara Kerja SNI

1. **Permintaan Klien**: Saat klien (misalnya, peramban web) memulai koneksi ke server, ia mengirimkan informasi SNI sebagai bagian dari *handshake* TLS. Informasi ini mencakup nama host (*hostname*) dari situs web yang ingin diakses.
2. **Respon Server**: Berdasarkan nama host yang diminta, server akan memilih sertifikat SSL yang sesuai untuk domain tersebut.
3. **Koneksi Aman**: Setelah sertifikat SSL dipilih, *handshake* TLS selesai, dan koneksi aman terbentuk antara klien dan server.

## Mengapa SNI Penting?

Tanpa SNI, sebuah server hanya dapat melayani satu sertifikat SSL per alamat IP. Jika ada beberapa situs web yang membutuhkan enkripsi TLS pada satu server atau satu alamat IP, SNI memungkinkan setiap situs web untuk memiliki sertifikat SSL sendiri, tanpa memerlukan alamat IP yang berbeda untuk masing-masing situs.

## Keuntungan dan Keterbatasan SNI

### Keuntungan

- **Menghemat IP**: Tidak perlu menggunakan banyak alamat IP untuk setiap domain.
- **Mengurangi Biaya**: Menghindari kebutuhan untuk membeli alamat IP tambahan.
- **Efisiensi Infrastruktur**: Hosting beberapa situs HTTPS di satu server lebih mudah dengan SNI.

### Keterbatasan

- **Kompatibilitas Perangkat Lama**: Beberapa perangkat dan peramban lama tidak mendukung SNI, yang dapat membatasi akses.
- **Dukungan Server**: Harus memastikan server yang digunakan mendukung SNI dan dapat melayani beberapa sertifikat SSL.

## Celah SNI terhadap HTTP Injection

Ada beberapa cara di mana SNI dapat dipengaruhi dalam konteks keamanan jaringan yang lebih luas. Konfigurasi yang tepat sangat penting untuk mencegah potensi serangan.

### Eksposur Nama Host

Informasi SNI dikirimkan dalam teks terbuka di *Client Hello* selama *handshake* TLS. Penyusup dapat melihat nama domain yang diminta, yang bisa membuka peluang untuk:

- **Melakukan Pemblokiran Konten (Content Filtering)**: Penyusup yang berada di antara koneksi (misalnya, *man-in-the-middle*) dapat memblokir atau mengarahkan lalu lintas ke alamat palsu berdasarkan nama domain yang ditemukan dalam SNI.
- **Menginjeksi Respon HTTP Tidak Sah**: Jika ada elemen HTTP yang tidak terenkripsi, penyerang dapat melakukan *HTTP injection* untuk menambahkan skrip atau konten berbahaya pada permintaan yang seharusnya aman.

## Contoh Kasus yang Memanfaatkan Celah SNI

Biasanya, SNI tidak digunakan untuk mengeksploitasi celah keamanan. Namun, ada beberapa kasus di mana informasi SNI dapat dimanfaatkan untuk tujuan jahat:

- **Pemblokiran Situs**: Penyusup dapat menggunakan informasi SNI untuk memblokir akses ke situs tertentu, seperti pemblokiran situs web yang dianggap tidak diinginkan atau berbahaya yang dikunjungi oleh pengguna (misalnya, **Internet Positif**).
- **Pencurian Informasi**: Penyusup dapat menggunakan informasi SNI untuk mengidentifikasi situs web yang dikunjungi oleh pengguna dan mencuri informasi sensitif yang dikirimkan melalui koneksi HTTPS (misalnya, informasi login, data pribadi, dll.).
