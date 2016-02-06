---
layout: post
title: Cara mengatur touchpad Elantech di Arch Linux
description: mengkonfigurasi touchpad elantech 
keywords: elantech, touchpad, linux
---

<img src="{{ site.baseurl }}/images/2015/08/Acer_CB5-311_series_touchpad.jpg" alt="touchpad" style="width: 350px;"/>

Udah pada pernah liat kan model touchpad seperti gambar diatas ? Yup, laptop keluaran terbaru sekarang sudah mengimplementasikan touchpad model tersebut. Tombol klik kiri/kanan sudah menyatu dengan touchpad, yang membuat tampilan touchpad ini terlihat simpel dan minimalis. Namun pada distro linux umumnya touchpad ini tidak terkonfigurasi dengan benar, contohnya seperti tidak bisa scrolling.

Nah, disini saya ingin membagi tutorial mengenai bagaimana Cara mengatur touchpad Elantech pada Arch Linux ( kenapa Arch Linux melulu sih ? yah, karena distro tersebut lah yang sedang saya gunakan ), sedangkan untuk distro lain anda tinggal menyesuaikan saja :D.

Buka terminal dan jalankan perintah berikut

    echo "options psmouse force_elantech=1" | sudo tee -a /etc/modprobe.d/psmouse.conf
    sudo rmmod psmouse &amp;&amp; sudo modprobe psmouse
    nano /etc/X11/xorg.conf.d/10-synaptics.conf

kemudian tambahkan baris di bawah ini :

    Section "InputClass"
        Identifier      "touchpad catchall"
        Driver          "synaptics"
        MatchIsTouchpad "on"
    
    Option "SHMConfig" "on"
    Option "VertEdgeScroll" "on"
    Option "HorizEdgeScroll" "on"
    Option "CornerCoasting" "on"
    Option "CoastingSpeed" "0.30"
    Option "VertTwoFingerScroll"   "on"
    Option "HorizTwoFingerScroll"  "on"
    Option "CircularScrolling" "off"
    Option "CricularTrigger" "0"
    Option "TapButton1" "1"
    Option "TapButton2" "2"
    Option "TapButton3" "3"
    Option "LTCornerButton" "2"
    Option "RTCornerButton" "2"
    EndSection

Nah sekarang coba restart sistemnya, dan sekarang anda sudah bisa menggunakan scrolling dengan touchpad anda. Untuk versi GUI, anda bisa menggunakan aplikasi gpointing-device-settings 😀

terima kasih.

[1]: {{ site.baseurl }}/images/2015/08/Acer_CB5-311_series_touchpad.jpg
