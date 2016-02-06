---
layout: post
title: konfigurasi adb di archlinux
description: kondigurasi android debug bridge di archlinux
keywords: adb, archlinux
---
Android Debug Bridge ( ADB ) adalah sebuah alat yang digunakan untuk mengendalikan emulator atau device android yang terhubung dengan usb. Tentunya bagi pecinta Android, ADB merupakan alat yang wajib untuk dimiliki di komputer anda. Tool ini sudah termasuk dalam paket Android SDK ( platform-tool ). Berikut tutorialnya :

#### Instalasi

**Android SDK :**

    wget https://aur.archlinux.org/packages/an/android-sdk/android-sdk.tar.gz
    tar -xvzf android-sdk.tar.gz
    cd android-sdk
    makepkg -si

**Android SDK Platfrom Tools :**

    wget https://aur.archlinux.org/packages/an/android-sdk-platform-tools/android-sdk-platform-tools.tar.gz
    tar -xvzf android-sdk-platform-tools.tar.gz
    cd android-sdk-platform-tools
    makepkg -si

**Set Owner And Add Group Of Android Directory :**

    sudo chown -R USER /opt/android-sdk
    sudo groupadd android
    sudo gpasswd -a USER android

**Change Permissions :**

    sudo chgrp -R android /opt/android-sdk
    sudo chmod -R g+w /opt/android-sdk
    sudo find /opt/android-sdk -type d -exec chmod g+s {};

**Android Udev :**

    wget https://aur.archlinux.org/packages/an/android-udev/android-udev.tar.gz
    tar -xvzf android-udev.tar.gz
    cd android-udev
    makepkg -si

Hubungkan Android kamu ke Komputer, kemudian jalankan perintah lsusb untuk melihat Id vendor dan product Android kamu.

setelah perintah dijalankan akan muncul informasi seperti ini.

![][1] 

Pada gambar diatas, tertera informasi **0fce:2149**, yang mana **0fce** merupakan sebuah Vendor Id dan **2149** merupakan Product Id.

Kemudian Tambahkan Rules untuk Device yang kita miliki.

    sudo nano /etc/udev/rules.d/51-android.rules

dan tambahkan baris dibawah ini.

    SUBSYSTEM=="usb", ATTR{idVendor}=="VENDOR ID", MODE="0666"
    SUBSYSTEM=="usb",ATTR{idVendor}=="VENDOR ID",ATTR{idProduct}=="PRODUCT ID",SYMLINK+="android_adb"
    SUBSYSTEM=="usb",ATTR{idVendor}=="VENDOR ID",ATTR{idProduct}=="PRODUCT ID",SYMLINK+="android_fastboot"

Ganti Vendor dan Product ID yang saya tebalkan diatas dengan Milik anda sendiri. kemudian save filenya dan jalankan perintah ini.

    sudo udevadm control --reload-rules

**Pengecekan :**
  
Untuk mengecek perangkat kamu sudah bisa digunakan atau tidak. jalankan perintah dibawah ini.

Jika muncul informasi seperti ini. itu berarti Device anda sudah siap digunakan dengan ADB 😀

![][2]


**Penggunaan :**

Untuk menggunakan ADB di linux caranya sama seperti cara penggunakan ADB pada umumnya.  
kamu bisa melihat informasi mengenai ADB dengan menjalankan perintah **"man adb"**

![][3]


[1]: {{ site.baseurl }}/images/2013/06/Screen_50.png
[2]: {{ site.baseurl }}/images/2013/06/Screen_51.png
[3]: {{ site.baseurl }}/images/2013/06/Screen_52.png
  

