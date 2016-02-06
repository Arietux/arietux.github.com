---
layout: post
title: sharing koneksi Wi-Fi melalui Wi-Fi di linux
description: share internet wifi melalui wifi
keywords: hotspot, sharing, linux, wifi
---

"*Sharing koneksi wifi melalui wifi ?*" bingung maksudnya ? atau kalimat tersebut pernah terlintas di pikiran anda ? coba perhatikan percakapan dibawah ini bagi yang masih bingung sama judul yang saya buat.

### Kronologi

Budi: Bro, gue ga bisa konek ke wifi kampus nih -_-  
Dhimas: Lha, kok bisa ?  
Budi : Mana gue tau -_-  
Dhimas : Kan bisa tethering dari HP andro lu bro ? 😀  
Budi : Yah, jaringannya lelet nih kalo di kampus, mana kuota gue udah mau habis lagi -_-  
Dhimas : Ya udah, gue share aja internet gw pake kabel LAN, bentar ya gue cek dulu kabelnya.  
Budi : Okeh 😀  
Dhimas : Yah, kabel LAN gue tinggal di rumah bro. 😀  
Budi : Di windows kan bisa share koneksi internet wifi bro, dibikin hotspot gitu laptopnya pake connectify -_-  
Dhimas : Yah, gw kan pake linux bro, gimana sih ? -_-  
Budi : Kan elu dualboot sama windows juga bro, tinggal reboot doang males amat jadi orang:D  
Dhimas : gw lagi ngerjain tugas nih, belum siap lagi. di windows kan kalo buka dokumen dari linux suka ngaco tulisannya.  
Budi : Ah elu mah tega amat sama temen sendiri, gw juga mau ngerjain tugas bingung nih ga ada koneksi internet T_T  
Dhimas : Ya udah bentar, gw googling dulu cara sharing koneksi wifi di linux  
Budi : Gitu dong bro :*

Jadi inti dari percakapan diatas, si Budi ini tidak bisa mengakses wifi kampus sedangkan temennya bisa, dan si Budi ini minta ke temennya si Dhimas untuk sharing koneksi internetnya. 😀

Kembali ke pokok pembahasan, artikel ini sebenarnya sangat berkaitan dengan cara membuat hotspot di linux, untuk membuat hotspot di linux kita bisa menggunakan software Network Manager, namun pada network manager ini kita tidak bisa sekaligus membuat hotspot saat kita sendiri sedang terhubung ke internet melalui interface Wi-Fi, beda cerita jika anda terkoneksi internet melalui interface LAN Card atau Modem USB, hal itu tentu bisa 😀

Nah, disisi lain jika anda menggunakan Windows, maka anda bisa sharing internet wi-fi melalui wi-fi dengan menggunakan software Connectify ( jika tidak ingin ribet ) atau bisa juga manual melalui Command Prompt. Tapi itu kan Windows ? Bagaimana jika anda menggunakan Linux ? Mari simak caranya di bawah ini 😀

### Persyaratan

* Pastikan perangkat Wi-Fi yang anda miliki support Access Point mode, anda bisa menuju ke url ini https://wireless.wiki.kernel.org/en/users/drivers. Atau bisa melalui perintah **iw list** di terminal.

![sharing koneksi wi-fi melalui wi-fi][1]

AP, menunjukan indikasi bahwa interface wi-fi anda support Access Point mode.

* AP mode tidaklah cukup, karena disini kita akan menggunakan satu interface Wi-Fi untuk membuat Hotspot sekaligus terkoneksi ke jaringan Wi-Fi di waktu yang bersamaan. untuk menggunakan fitur ini, maka hasil **iw list** harus seperti gambar dibawah.  
![sharing wifi melalui wifi][2]  
`#channels <= 1` , artinya Hotspot yang anda buat harus berada pada channel yang sama dengan hotspot yang terkoneksi pada laptop anda.

### Tools

Untuk sharing wi-fi melalui wi-fi atau membuat laptop kita sebagai Hotspot dan terkoneksi ke jaringan Wi-Fi di saat yang bersamaan bisa menggunakan hostapd,dnsmasq, dan iptables. Namun menggunakan hostapd itu sedikit tricky 😀 . Jadi kita akan menggunakan tool **[Create_AP][3]** yang mengkombinasikan hostapd,dnsmasq, dan iptables ( mudah dan simpel ).

### Dependensi

* bash
* util-linux
* procps atau procps-ng
* hostapd
* iproute2
* iw
* iwconfig ( instal ini, jika perintah **iw** tidak mengenali perangkat jaringan anda )
* haveged
* dnsmasq
* iptables

### Instalasi

**Umum :**

    git clone https://github.com/oblique/create_ap 
    cd create_ap 
    make install

**Arch Linux :**

    yaourt -S create_ap

**Gentoo :**

    emerge layman
    layman -f -a jorgicio
    emerge net-wireless/create_ap

### Cara Penggunaan

**Sharing koneksi internet dari interface LAN Card**

    create_ap wlan0 eth0 namahotspot password

**Sharing koneksi internet dari modem usb**

    create_ap wlan0 ppp0 namahotspot password

**Sharing koneksi internet dari Wireless Card yang sama**

    create_ap wlan0 wlan0 namahotspot password

Dan masih banyak lagi fitur-fitur yang dimiliki **create_ap** ini, lebih lengkapnya silahkan kunjungi halamannya disini https://github.com/oblique/create_ap

![sharing wi-fi melalui wifi][4]

Sharing koneksi internet ( membuat hotspot ) saat sedang terkoneksi jaringan wifi.

Sekianlah dari saya atas artikel ini, semoga bermanfaat bagi anda. Saya mohon maaf jika ada kata pada artikel ini yang kurang berkenan di hati anda baik sengaja maupun tak di sengaja.

Terimakasih.

Referensi :  
https://github.com/oblique/create_ap  
http://superuser.com/questions/649220/a-wifi-ap-with-a-single-nic  
https://wiki.archlinux.org/index.php/Software_access_point#Requirements  
http://askubuntu.com/questions/72989/how-to-share-my-wifi-internet-via-wifi

[1]: http://www.kawainaaa.com/wp-content/uploads/2015/09/Screenshot_2015-09-09_01-08-11.png
[2]: http://www.kawainaaa.com/wp-content/uploads/2015/09/Screenshot_2015-09-09_01-17-50.png
[3]: https://github.com/oblique/create_ap
[4]: http://www.kawainaaa.com/wp-content/uploads/2015/09/Screenshot_2015-09-09_01-17-20-300x121.png