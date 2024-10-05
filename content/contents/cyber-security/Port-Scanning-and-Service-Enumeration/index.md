---
title: Port Scanning and Service Enumeration
date: 2024-08-25
categories: [Pentesting]
tags: [Security, Reconnaissance]
---

Pada tahap **Active Reconnaissance**, penyerang akan melakukan scanning secara langsung terhadap target untuk mengumpulkan informasi lebih lanjut. Dalam tahap ini, penyerang akan mencari informasi tentang port yang terbuka, layanan yang berjalan, dan versi perangkat lunak yang digunakan oleh target. Dua teknik utama yang digunakan dalam Active Reconnaissance adalah **Port Scanning** dan **Service Enumeration**.

## Port Scanning
Biasanya, target memiliki beberapa port yang terbuka untuk menerima koneksi. Port ini digunakan untuk berbagai layanan seperti `HTTP`, `FTP`, `SSH`, dll.

Tools yang umum digunakan untuk melakukan port scanning adalah:
- **Nmap**: Network Mapper, tool open source yang sangat populer untuk scanning jaringan.
- **Masscan**: Tool yang dirancang untuk melakukan scanning port secara cepat.
- **Zmap**: Tool yang dirancang untuk melakukan scanning port secara skala besar.
- **Hping**: Tool yang dirancang untuk melakukan scanning port dengan teknik yang berbeda.
- **Netcat**: Tool yang digunakan untuk melakukan scanning port dan juga berfungsi sebagai *backdoor*.

Dalam kasus ini, kita akan melakukan simulasi menggunakan `Nmap` untuk melakukan scanning port terhadap target `192.168.1.1` yaitu hardware router yang terhubung ke jaringan lokal.
`
{{< alert >}}
pastikan telah melakukan *Passive Reconnaissance* sebelum melakukan *Active Reconnaissance*.
{{< /alert >}}

```bash
$ nmap -T5 192.168.1.1
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-25 12:15 WIB
Stats: 0:00:02 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 30.13% done; ETC: 12:15 (0:00:07 remaining)
Nmap scan report for 192.168.1.1
Host is up (0.0097s latency).
Not shown: 997 closed tcp ports (conn-refused)
PORT    STATE SERVICE
21/tcp  open  ftp
80/tcp  open  http
443/tcp open  https

Nmap done: 1 IP address (1 host up) scanned in 2.71 seconds
```

Dari hasil scanning di atas, kita mengetahui bahwa target memiliki 3 port yang terbuka, yaitu:
- Port 21: FTP
- Port 80: HTTP
- Port 443: HTTPS

## Service Enumeration

Berlanjut dari hasil port scanning, kita dapat melakukan service enumeration untuk mengetahui versi perangkat lunak yang digunakan oleh target. Informasi ini dapat membantu penyerang dalam mengeksploitasi kerentanan yang ada pada versi perangkat lunak tersebut.

```bash
$ nmap -sV -T5 192.168.1.1
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-25 12:17 WIB
Nmap scan report for 192.168.1.1
Host is up (0.010s latency).
Not shown: 997 closed tcp ports (conn-refused)
PORT    STATE SERVICE  VERSION
21/tcp  open  ftp      vsftpd 2.3.4
80/tcp  open  http     nginx
443/tcp open  ssl/http nginx
Service Info: OS: Unix

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 21.05 seconds
```

Dari hasil service enumeration di atas, kita mengetahui bahwa:
- Port 21: FTP menggunakan `vsftpd 2.3.4`
- port 80 dan 443: Menggunakan `nginx` sebagai web server.
- Sistem operasi yang digunakan adalah `Unix`.

Dengan informasi ini, kita mendapatkan versi yang di tampilkan oleh target, sehingga kita dapat mencari kerentanan yang ada pada `vsftpd 2.3.4`.

Dengan melakukan port scanning dan service enumeration, penyerang dapat mengumpulkan informasi yang cukup untuk melanjutkan ke tahap selanjutnya dalam proses *penetration testing*.

> **Catatan**: Pada proses Scanning dan Enumeration, ada kondisi dimana terdapat kondisi yang tidak diinginkan seperti *false positive* atau *false negative*. Oleh karena itu, perlu dilakukan validasi lebih lanjut untuk memastikan hasil scanning yang akurat.
{: .prompt-info }

Demikianlah penjelasan singkat tentang Port Scanning dan Service Enumeration. Semoga bermanfaat!
dan tetap explore dan belajar lebih lanjut.