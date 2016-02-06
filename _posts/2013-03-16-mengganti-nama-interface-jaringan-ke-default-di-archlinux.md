---
layout: post
title: mengubah nama kartu jaringan ke semula di archlinux
description: mengubah nama kartu jaringan ke semula di archlinux
keywords: archlinux, kartu jaringan, enp3s0, wlp2s0
---

> Update: Semenjak systemd v209, nama rulesnya di ganti menjadi
> 80-net-setup-link.rules

Selamat sore gan 😀  
Sebenarnya artikel ini sudah di draft 3 hari yang lalu setelah install ulang Archlinux saya yang 32bit ke 64bit, saya install ulang karena RAM saya cuma terdeteksi 3,3GB di archlinux 32bit, maka dari itu saya install ulang ke 64bit biar RAM terdeteksi dengan sempurna 😀

Waktu install ulang, saya menggunakan ISO archlinux 2013.03.01, entah kenapa sewaktu installasi ada yang janggal, yaitu nama interface jaringan yang berubah. Saya keliling keliling di forum archlinux, ternyata terdapat bug di ISO ini. Mau gimana lagi, saya install aja archlinuxnya, setelah installasi pun ternyata nama interfacenya pun tetap tidak berubah.

Interface yang berubah adalah :  
**eth0** menjadi **enp3s0f0**  
**wlan0** menjadi **wlp2s0**

Kemudian keliling keliling forum archlinux, ternyata dapet pencerahan. untuk mengembalikan nama interface jaringan kita perlu membuat file **80-net-setup-link.rules** di folder **/etc/udev/rules.d/**

{% highlight sh %}
sudo ln -s /dev/null /etc/udev/rules.d/80-net-setup-link.rules
{% endhighlight %}

atau bisa juga dengan menambahkan baris **net.ifnames=0 ** di kernel line, seperti gambar dibawah ini.

![][1]

Untuk informasi lebih lanjut silahkan menuju ke [halaman ini][2]

[1]: http://www.kawainaaa.com/wp-content/uploads/2013/03/Screenshot-2Bfrom-2B2014-08-15-2B09-3A49-3A17.png
[2]: http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames
