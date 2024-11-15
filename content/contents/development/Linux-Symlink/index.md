---
title: Linux Symbolic Link
date: 2024-11-15
categories: [Development, DevOps]
tags: [Linux, System]
---

# Linux Symbolic Link
Linux Symbolic Link adalah sebuah file yang mengarah ke referensi file atau direktori tanpa harus membuat salinan dari file atau direktori tersebut.

{{<mermaid>}}
graph TD
    A[File Asli <br>/home/user/original.txt]
    B[Symbolic Link <br>/home/user/link.txt]
    
    A -->|Destionation| B
{{</mermaid>}}

## Membuat Symbolic Link
```bash
ln -s [source] [destination] 
```
- `source` : file atau direktori yang akan di-link.
- `destination` : nama symbolic link yang akan dibuat.
> flag `-s` digunakan untuk membuat symbolic link. lihat `man ln` untuk informasi lebih lanjut.

### Contoh Symbolic Link
```bash
ln -s /home/user/original.txt /home/user/link.txt
```
{{<alert>}}
Pastikan `source` dan `destination` harus memiliki path yang benar.
{{</alert>}}

## Membuat Hard Link
```bash
ln [source] [destination]
```

### Contoh Hard Link
```bash
ln /home/user/original.txt /home/user/link.txt
```


## Hard Link vs Symbolic Link
- **Hard Link** : mengarah ke file asli. Jika file asli dihapus, hard link masih bisa diakses.
- **Symbolic Link** : mengarah ke path file asli. Jika file asli dihapus, symbolic link tidak bisa diakses.

{{< alert cardColor="#e63946" iconColor="#1d3557" textColor="#f1faee" >}}
`Hard link` tidak bisa digunakan untuk direktori. Jika ingin membuat link ke direktori, gunakan `symbolic link`.
{{< /alert >}}
