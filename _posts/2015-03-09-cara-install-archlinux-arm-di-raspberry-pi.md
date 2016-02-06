---
layout: post
title: install archlinux arm di raspberry pi 2
description: panduan instalasi archlinux arm di raspberry pi 2
keywords: archlinux, arm, raspberry pi 2
---
![arch linux arm logo][1]

Berikut merupakan cara installasi Archlinux Arm pada Raspberry Pi 2.

**CATATAN :**  
- Disini saya menggunakan distro linux sebagai media installasi archlinux arm di sdcard untuk raspberry pi  
- Setelah installasi ini, sdcard tidak perlu di resize lagi untuk mendapatkan keseluruhan size partisi  
- **sdX** dan **mmcblkX** adalah penamaan device dari sdcard. jika menggunakan adapter micro sdcard, maka nama device sdcardnya **mmcblkX**. dan jika menggunakan card reader, maka nama device sdcardnya **sdX**

1\. Jalankan fdisk untuk pemartisian SD card:  

2\. Setelah memasuki fdisk, hapus partisi lama dan buat partisi baru:
    * Ketik **o**. opsi ini akan menghapus semua partisi yang ada di SD card
    * Ketik **p** untuk melihat daftar partisi.
    * Ketik **n**, kemudian **p** untuk membuat partisi primary, **1** untuk partisi pertama di dalam disk, tekan ENTER untuk **Default first sector**. kemudian ketik **+100M** untuk **the last sector**.
    * Ketik **t**, kemudian **c** untuk menerapkan tipe partisi pertama ke W95 FAT32 (LBA).
    * ketik **n**, kemudian **p** untuk partisi primary, dan **2** untuk partisi kedua di dalam disk. dan kemudian tekan ENTER dua kali untuk menerima **default first and last sector**
    * tulis tabel partisi yang telah dibuat dan keluar dengan mengetik **w**

3\. Buat dan mount berkas system FAT:  

    mkfs.vfat /dev/mmcblk0p1
    mkdir boot
    mount /dev/mmcblk0p1 boot

4\. Buat dan mount berkas sister ext4:  

    mkfs.ext4 /dev/mmcblk0p2
    mkdir root
    mount /dev/mmcblk0p2 root

5\. Download dan ekstrak berkas sistem akar ( sebagai administrator, bukan melalui sudo ):  

    wget http://archlinuxarm.org/os/ArchLinuxARM-rpi-2-latest.tar.gz
    bsdtar -xpf ArchLinuxARM-rpi-2-latest.tar.gz -C root
    sync

6\. Pindahkan berkas boot ke partisi pertama:  

7\. unmount kedua partisi:  

8\. Masukkan SD card ke dalam Raspberry pi, hubungkan kabel ethernet dan tancapkan power 5V

9\. Gunakan ssh untuk mengendalikan Raspberry Pi.

Referensi :  

 - http://archlinuxarm.org/platforms/armv7/broadcom/raspberry-pi-2

[1]: http://www.kawainaaa.com/wp-content/uploads/2015/03/Logo_of_Arch_Linux_ARM-300x67.png
