---
layout: post
title: install yourt di archlinux
description: packet manager aur di archlinux
keywords: yourt, pacman, archlinux
---

**Yaourt** ( Yet An Other User Repository Tool ) merupakan AUR package manager, yang berguna untuk menginstal paket-paket aplikasi yang berada di repository AUR. Aplikasi ini juga merupakan aplikasi yang akan saya instal pertama kali setelah selesai proses instalasi arch linux.

### Contoh perintah

Mencari aplikasi yang ingin di install, contohnya paket linux :

Mengupdate paket aplikasi yang di instal dari AUR :

### Instalasi Yaourt

1\. ubah file pacman.conf

    [archlinuxfr]
    SigLevel = Never
    Server = http://repo.archlinux.fr/$arch

2\. instal yaourt

    sudo pacman -Syu
    sudo pacman -S yaourt

#### Penyelesaian Masalah

Jika saat di tengah proses kompil aplikasi terhenti dengan error "application: there is no enough space on /tmp", hal ini disebabkan karena yaourt menggunakan **/tmp ** (di mount sebagai **tmpfs** ) untuk mengkompil aplikasi. **tmpfs** sendiri adalah file system yang secara default menggunakan 50% RAM. jadi hal ini paling sering dijumpai oleh laptop/komputer yang memiliki ukuran RAM yang rendah.

Hal tersebut bisa disiasati dengan cara mengatur **tmpdir** pada file /etc/yaourtrc, dengan mengubah/menambahkan baris berikut :

    TMPDIR="/customtmp" # sesuaikan folder

Maka selesailah sudah proses instalasi aplikasi yaourt ini, untuk informasi lebih lengkap silahkan lihat referensi dibawah.

Terimakasih.

Referensi :  
https://wiki.archlinux.org/index.php/Yaourt#Installation
