---
layout: post
title: pemasangan cisco packet tracer di ubuntu 15.04
description: instalasi cisco packet tracer
keywords: packettracer, ubuntu, 15.04
---
<img src="{{ site.baseurl }}/images/2015/06/Screenshot-from-2015-06-12-222249.png" alt="preview" style="width: 350px;"/>

Cisco Packet Tracer pada dasarnya adalah sebuah aplikasi simulator yang memungkinkan kita untuk berlatih serta belajar mengenai cisco router tanpa harus membeli alat yang umumnya memiliki harga yang mahal.

Pada kesempatan kali ini saya akan menjabarkan bagaimana cara Pemasangan Cisco Packet Tracer di Ubuntu 15.04.

### Persiapan

Pertama kali yang harus dilakukan tentunya dengan mengunduh berkas Cisco Packet Tracer 6.1.1 versi Pelajar _**[Disini][2]**_

### Langkah – Langkah

1\. Ekstrak terlebih dahulu hasil file hasil download, atau bisa juga menggunakan perintah terminal.

    tar xzf cisco-packet-tracer.tar.gz

2\. Masuk ke dalam folder tersebut dan beri hak akses eksekusi pada file install, kemudian jalankan perintah untuk pemasangan Cisco Packet Tracer

    cd folderpackettracer
    chmod +x install
    sudo ./install

3\. kemudian anda akan diminta untuk menyetujui _**EULA**_, tekan tombol enter untuk membaca _**EULA**_ kemudian Ketik _**Y**_ dan _**enter**_.

4\. selanjutnya anda akan diminta menginputkan letak installasi Packet Tracer, tekan _**enter**_ untuk opsi default.

5\. kemudian ketik _**Y**_ untuk membuat symbolic link.

### Permasalahan ( bagi distro 64bit )

Oke, setelah installasi saya menemukan masalah sedikit yaitu Cisco Packet Tracer tidak berjalan setelah di eksekusi. permasalahannya ada pada dependency yang kurang yaitu `libssl1.0.0:i386` dan `libqtwebkit4:i386`. setelah anda menginstall paket tersebut maka Cisco Packet Tracer akan berjalan tanpa gangguan.

Sekian dan Terima Kasih.

[2]: https://drive.google.com/uc?export=download&amp;confirm=S5Mt&amp;id=0B9IVGyxtTpZZVnBQSjJQZ0VHSUk
  
