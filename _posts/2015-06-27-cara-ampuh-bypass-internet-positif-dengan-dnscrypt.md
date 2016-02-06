---
layout: post
title: Cara ampuh bypass internet positif dengan dnscrypt
description: membypass internet positif menggunakan dnscrypt
keywords: arch, bypass, dnscrypt, linux, unbound
---

![internet positif][1]

Pernahkah anda terjebak ke halaman Internet Positif ? sebagian besar pengguna komputer pasti pernah terjebak ke situs ini saat hendak mengunjungi situs tersayang anda. Bahkan untuk pengguna speedy, membypass internet positif dengan menggunakan ssh tunnel tidak berpengaruh sama sekali. Nah di post ini saya akan memberi Cara ampuh bypass internet positif dengan menggunakan dnscrypt.

**Install Dnscrypt & Unbound**

    sudo pacman -S dnscrypt-proxy dnscrypt-autoinstall unbound

autobound disni berfungsi sebagai dns caching, guna untuk mempercepat pengakses-an situs.

**Konfigurasi :**

konfigurasi resolv.conf

    sudo echo "nameserver 127.0.0.1" > /etc/resolv.conf
    sudo chattr +i /etc/resolv.conf

tambahkan baris di bawah ini di akhir baris pada file /etc/unbound/unbound.conf

    do-not-query-localhost: no
       forward-zone:
       name: "."
       forward-addr: 127.0.0.1@40

kemudian ubah baris pada file `/etc/conf.d/dnscrypt-proxy` seperti ini dibawah ini

    DNSCRYPT_LOCALIP=127.0.0.1
    DNSCRYPT_LOCALPORT=40

setelah itu ubah DNSCrypt resolver dengan menjalankan dnscrypt-autoinstall.

![dnscrypt][2]

kemudian ketik **y** dan **enter**. setelah itu muncul pilihan dnscrypt service, disini saya pilih OpenDNS.

![dnscrypt][3]

setelah itu jalankan service dnscrypt dan unbound

    sudo systemctl start dnscrypt-proxy unbound

kemudian uji coba apakah dnscrypt berhasil berjalan dengan sempurna.

![dnscrypt][4]

[1]: http://www.kawainaaa.com/wp-content/uploads/2015/06/Screenshot_2015-06-27_19-20-21.png
[2]: http://kawainaaa.com/wp-content/uploads/2015/06/Screenshot_2015-06-27_19-07-19-300x71.png
[3]: http://kawainaaa.com/wp-content/uploads/2015/06/Screenshot_2015-06-27_19-08-38-300x152.png
[4]: http://kawainaaa.com/wp-content/uploads/2015/06/Screenshot_2015-06-27_19-13-37-300x102.png
