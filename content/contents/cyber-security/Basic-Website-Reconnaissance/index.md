---
title: Basic Website Reconnaissance
date: 2024-08-24
categories: [Cyber Security]
tags: [Security, Reconnaissance]
---

Konsep **reconnaissance** adalah tahap awal dalam proses penilaian keamanan atau hacking yang bertujuan untuk mengumpulkan informasi sebanyak mungkin tentang target. Ini adalah langkah kunci yang membantu penyerang atau penilai keamanan memahami struktur, konfigurasi, dan potensi kerentanannya.

Dalam Reconnaissance terbagi menjadi 2 yaitu:

1. **Passive Reconnaissance**
Mengumpulkan informasi tanpa berinteraksi langsung. Dengan penggumpulan data basic pada sebuah target, yang meliputi seperti **CDN**, **IP Scan**, **Technology in used**, dan arsitektur jaringan yang terexpose.
Dengan menggunakan Passive scanning, tentunya memiliki kelebihan, yaitu senyap. Yang dimana Target tidak akan melakukan Logging data akses atau membaca footprint penyerang. Namun tidak seaggresive Active Scan

1. **Active Reconnaissance**
Mengumpulkan informasi dengan secara langsung berinteraksi dengan target. yang meliputi [**Port Scanning**](/posts/portscan-and-service-enum/), [**Service Enumeration**](/posts/portscan-and-service-enum/) dan **Path Enumeration**.
Dalam hal Active Scan, tentunya jejak penyerang akan terlihat oleh target dengan sangat mudah untuk tracing sumber penyerang atau pun footprint yang ditinggal oleh penyerang, seperti apa saja yang diakses atau mencoba masuk.

## Cara Melakukan Passive Scanning

### Search Online
**Penjelasan:**  
Mencari informasi tentang target melalui sumber-sumber online dapat memberikan wawasan awal yang penting. Ini bisa termasuk informasi yang dipublikasikan di media sosial, forum, atau situs web lainnya.

**Cara:**
1. **Gunakan Mesin Pencari:**  
   Cari nama target, domain, atau IP menggunakan mesin pencari seperti Google. Gunakan query spesifik seperti `"targetname site:example.com"` untuk menemukan informasi yang relevan.
2. **Periksa Media Sosial:**  
   Teliti profil media sosial, postingan, atau komentar yang mungkin mengungkapkan informasi tentang target atau teknologi yang digunakan.
3. **Cek Forum dan Blog:**  
   Telusuri forum atau blog yang mungkin membahas tentang target atau teknologi yang digunakan oleh target.

### Whois Lookup
**Penjelasan:**  
WHOIS lookup memberikan informasi tentang pendaftaran domain, seperti pemilik, tanggal pendaftaran, dan server DNS. Ini dapat membantu dalam mengidentifikasi pemilik atau afiliasi domain.

**Cara:**
1. **Gunakan Perintah WHOIS:**  
   Jalankan `whois <domain>` di terminal atau gunakan layanan WHOIS online.
2. **Analisis Informasi WHOIS:**  
   Catat detail seperti alamat pendaftar, email kontak, dan server DNS. Ini dapat memberikan petunjuk tambahan tentang target.

### Mapping Target
**Penjelasan:**  
Mapping target melibatkan pemetaan dan pemahaman struktur dan arsitektur target untuk mengidentifikasi komponen atau layanan yang mungkin tersedia.

**Cara:**
1. **Identifikasi Subdomain:**  
   Gunakan alat seperti `sublist3r` untuk menemukan subdomain yang mungkin terkait dengan target.
2. **Peta Situs:**  
   Jika tersedia, ambil dan periksa peta situs dari target untuk mendapatkan daftar URL dan direktori yang mungkin ada.

---

## Cara Melakukan Active Scanning

### Port Scanning
**Penjelasan:**  
Port scanning adalah teknik untuk mengidentifikasi port yang terbuka di target dan layanan yang berjalan di port-port tersebut.

**Cara:**
1. **Gunakan Nmap:**  
   - **Basic Scan:** `nmap <target>` – Memindai port yang umum.
   - **Custom Port Scan:** `nmap -p 1-65535 <target>` – Memindai semua port.
   - **Service Version Detection:** `nmap -sV <target>` – Menampilkan versi layanan yang berjalan di port yang terbuka.
2. **Gunakan Netcat:**  
   `nc -zv <target> <port>` – Memeriksa port terbuka satu per satu.

### Service Enumeration
**Penjelasan:**  
Service enumeration adalah proses mengidentifikasi layanan yang berjalan pada port yang terbuka dan versi spesifik dari layanan tersebut.

**Cara:**
1. **Gunakan Nmap:**  
   - **Deteksi Versi Layanan:** `nmap -sV <target>` – Mengidentifikasi versi layanan.
   - **Deteksi OS:** `nmap -O <target>` – Mengidentifikasi sistem operasi yang digunakan.
2. **Gunakan Banner Grabbing:**  
   Dapat dilakukan dengan tools seperti `netcat` atau `telnet` untuk mengambil banner yang biasanya mencantumkan informasi versi layanan.

### Path Enumeration
**Penjelasan:**  
Path enumeration mencari direktori dan file tersembunyi di server web yang dapat memberikan informasi atau akses lebih lanjut.

**Cara:**
1. **Gunakan Dirb:**  
   - **Basic Scan:** `dirb http://<target>` – Mencari direktori dan file dengan wordlist default.
2. **Gunakan Gobuster:**  
   - **Basic Scan:** `gobuster dir -u http://<target> -w <wordlist>` – Mencari path yang tersembunyi menggunakan wordlist yang ditentukan.