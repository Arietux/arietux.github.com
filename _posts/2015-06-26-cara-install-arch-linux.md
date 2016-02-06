---
layout: post
title: Cara Install Arch Linux
description: panduan untuk pemasangan distro archlinux
keywords: archlinux, linux
---

Arch Linux merupakan distribusi linux yang berfokus pada kesederhanaan dan minimalisme. Selain itu, Arch Linux memiliki dokumentasi yang sangat lengkap serta rolling release. Rolling Release disini maksudnya, kita hanya perlu mengupdate paket agar sistem Arch Linux terbaharui, tidak perlu menunggu waktu 6 bulan untuk mendapatkan versi terbaru dari aplikasi yang terpasang.

Saya sendiri sudah menggunakan Arch Linux sejak tahun 2012 silam, yang saya suka dari Arch Linux selain dari dokumentasi dan rolling release yaitu sistem managemen paket Pacman ( Package Manager ) yang mudah digunakan, serta Repository pihak ke tiga yang sangat lengkap akan aplikasinya.

Karena Arch Linux berfokus pada kesederhanaan serta minimalisme, metode installasi Arch Linux tidak menggunakan GUI ( Graphical User Interface ) atau tidak ada istilah "klik klik klik… selesai". Untuk installasi archlinux kita hanya berhadapan dengan CLI ( Command Line Interface ). Namun disinilah letak kesenangannya, disini kita bisa lebih cepat mengetahui tentang installasi Linux dari dasar, yang dimulai dari pemartisian sampai tahap penginstallan Desktop Environment semua di jalankan melalui Terminal.

Oke, saya rasa cukup penjelasan saya mengenai Arch Linux. Mari kita mulai proses installasinya 😀

#### Persiapan

Segala sesuatu mesti ada persiapan, agar tidak tersesat di tengah jalan. Berikut persiapan-persiapan yang harus dilakukan sebelum memulai proses installasi Arch Linux.

 - ISO Arch Linux. Anda bisa mengunduh ISO Archlinux melalui website
   Kambing.UI disini http://kambing.ui.ac.id/iso/archlinux 
 - Pembuatan bootable USB Arch Linux, tahun 2015 masih pakai "DVD/CD-ROM" ? apa kata dunia!!. Oke untuk pembuatan bootable USB di Windows kita bisa  menggunakan Rufus. Sedangkan di Linux kita menggunakan perintah DD.  
   
   > dd bs=4M if=/letak/file/iso/archlinux.iso of=/dev/sdX && sync
   
   sebagai catatan, **/dev/sdX**  merupakan alamat flash disk anda.
   
 - Koneksi Internet yang kencang. "Internet kencang buat apa ? buat
   install arch linux pak". Yup, Installasi Arch Linux memerlukan koneksi yang stabil dan kencang. kenapa begitu ? ya ga papa sih,  semakin kencang kan semakin cepat kita merasakan Arch Linux terpasang di Laptop kita 😀  
 - Minuman/Cemilan, ini digunakan untuk mengisi waktu luang anda. Nah bagi yang internetnya agak lola, siap siap beli Minuman/Cemilan yang banyak ya 😀  
 - Pastikan Data penting anda sudah
   di backup, guna mencegah hilangnya data karena kesalahan yang anda
   perbuat. "Do With Your Own Risk!"


#### Pemartisian

Umumnya Linux dapat di install hanya dengan menggunakan 1 partisi root saja. namun disini saya menyiapkan partisi apa yang akan dibuat nanti.

| Name      | Mount Point | Type       |
| --------- | ----------- | ---------- |
| /dev/sda1 | /boot       | ext4       |
| /dev/sda5 | swap        | Linux Swap |
| /dev/sda6 | /var        | reiserfs   |
| /dev/sda7 | /           | ext4       |

####Install Arch Linux

Di tahap ini saya asumsikan anda sudah memasuki lingkungan Arch Linux terlepas anda memilih arsitektur x86_64 atau i686. Jalankan baris Perintah dibawah ini dan cermati  terlebih dahulu sebelum di eksekusi.

**Mengatur Layout Keyboard :**

**Membuat Partisi :**

    fdisk /dev/sda
    
    A. Create '/boot' partition (512 MiB)
    
    - Press 'm' for help
    - type 'n' then press enter to create/add a new partition
    - type 'p' then press enter for primary partition type
    - press 'enter' (default is 1) for partition number
    - type '2048' then press enter for first sector
    - type '+512M' for partition size for last sector
    
    Set bootable flag for /boot partition
    
    - type 'a' then press enter for toggle bootable flag
    - type '1' then press enter for partition number
    
    Print the partition table
    
    - type 'p' then press enter
    
    B. Create extended partition
    
    - Press 'm' for help
    - type 'n' then press enter
    - type 'e' then press enter for extended partition type
    - press 'enter' (default is 2) for partition number
    - press 'enter' (default) for first sector
    - press 'enter' (default is max) for partition size and last sector
    
    Print the partition table
    
    - type 'p' then press enter
    
    C. Create swap partition (2 GiB)
    
    - Press 'm' for help
    - type 'n' then press enter to create/add a new partition
    - type 'l' then press enter for logical partition type
    - press 'enter' (default) for first sector
    - type '+2G' for partition size for last sector
    
    Set 'linux swap' system id for swap partition
    
    - type 't' then enter
    - type '5' for partition number
    - type '82' for Hex Code
    
    Print the partition table
    
    - type 'p' then press enter
    
    D. Create "/var" partition (20 GiB)
    
    - Press 'm' for help
    - type 'n' then press enter to create/add a new partition
    - type 'l' then press enter for logical partition type
    - press 'enter' for first sector
    - type '+25G' for partition size for last sector
    
    Print the partition table
    
    - type 'p' then press enter
    
    E. Create root ("/") partition (sisanya)
    
    - Press 'm' for help
    - type 'n' then press enter to create/add a new partition
    - type 'l' then press enter for logical partition type
    - press 'enter' for first sector
    - press 'enter' (default is max) for partition size for last sector
    
    Print the partition table
    
    - type 'p' then press enter
    
    F. Write the partition table to disk
    
    - type 'w' then press enter


**Format Partisi :**

    mkfs.ext4 -L "boot" /dev/sda1
    mkswap -L "swap" /dev/sda5
    mkfs.reiserfs -l "var" /dev/sda6
    mkfs.ext4 -L "root" /dev/sda7

**Mount Partisi :**

    mount -t ext4 -o defaults,noatime /dev/sda7 /mnt
    mkdir -p /mnt/{boot,var}
    mount -t ext4 -o defaults,noatime /dev/sda1 /mnt/boot
    mount -t reiserfs -o rw,notail,nodiratime,noatime /dev/sda6 /mnt/var
    swapon -p 0 -L "swap"

**Pengecekan Partisi :**

    mount | grep '^/dev/sda'
    df -h | grep '^/dev/sda'
    swapon -s

**Menyambung Ke Internet :**

A. Melalui WiFi card

untuk **interface-wifi**, biasa di varian ubuntu nama interfacenya adalah ( wlan ) tetapi di Arch Linux untuk penamaan interface berbeda. silahkan di cek terlebih dahulu menggunakan perintah "ifconfig -a". untuk interface wireless, nama interface akan diawali dengan **wlp**, pada contoh kasus saya. nama interfacenya adalah **"wlp2s0"**. setelah menjalankan perintah wifi-menu, anda akan di minta memasukkan password wifi.

B. Melalui Etherned Card

    dhclient interface-ethernet


untuk **interface-ethernet**, adalah interface ethernet ( eth0 ). untuk di Arch Linux nama interface akan di awali dengan **enp**, pada contoh kasus saya. nama interface ethernetnya adalah "**enp3s0f0**".

C. Melalui USB Modem

kemudian edit file **/etc/wvdial.conf**

    [Dialer Defaults]
    Init2 = ATQ0 V1 E1 S0=0 &amp;C1 &amp;D2 +FCLASS=0
    Init3 = AT+CGDCONT=1,"IP,"3data"
    Modem Type = Analog Modem
    Phone = *99#
    ISDN = 0
    Username = 3data
    Init1 = ATZ
    Password = 3data
    Modem = /dev/ttyUSB0
    Baud = 9600

jalankan wvdial

tes koneksi :

jika sudah ada reply, maka kita lanjutkan ke tahap berikutnya.

**Install Paket Sistem :**

    pacstrap /mnt base base-devel
    pacstrap /mnt -Sy

**Membuat file fstab :**

    genfstab -p -U /mnt >> /mnt/etc/fstab

####Memasuki Lingkungan Chroot : 

**Install bootloader :**

    pacman -Sy grub-bios os-prober
    grub-install \--target=i386-pc \--recheck \--debug /dev/sda
    cp /usr/share/locale/en@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo
    grub-mkconfig -o /boot/grub/grub.cfg

**Menginstall Aplikasi Pendukung**

    pacman -Sy net-tools wget dhclient wvdial usb_modeswitch wpa_supplicant dialog


####Menginisial RAM DISK :

**Atur Password :**

kemudian masukan password anda 2 kali.

**Keluar dari lingkungan Chroot :**

**Melepas kaitan partisi :**

    umount /mnt/{boot,var}
    umount /mnt

kemudian reboot mesin anda

#### Konfigurasi Lanjutan

Sekarang masuk ke sistem dengan user **root**dan password yang anda buat tadi.

**Atur nama host :**

    hostnamectl set-hostname kawainaa-host

**Atur Bahasa Lokal :**

kemudian cari baris di bawah ini kemudian hapus **Hashtag/Pagar** di depan baris.

* "en_US.UTF-8 UTF-8"
* "en_US ISO-8859-1"
* "id_ID.UTF-8 UTF-8"
* "id_ID ISO-8859-1"

kemudian simpan dan jalankan perintah dibawah ini

    locale-gen
    nano /etc/locale.conf

setelah itu tambahkan baris dibawah ini :

    LANG="en_US.UTF8"
    LC_COLLATE=C
    LC_TIME=id_ID.UTF8

kemudian simpan.

**Atur Zona Waktu :**

    timedatectl set-timezone Asia/Jakarta

**Atur Jam dan Tanggal :**

    timedatectl set-time "2015-08-26 15:46:00"

untuk mensingkronisasi jam pada bios anda :

    timedatectl set-local-rtc 1

**Menambahkan pengguna baru :**

    useradd -m -g users -G wheel,games -s /bin/bash namauser

kemudian atur kembali password untuk pengguna yang baru dibuat

setelah itu masukkan pengguna tersebut ke daftar sudoers, agar dapat mengakses sistem administrasi.

    echo "arietux ALL=(ALL) ALL" >> /etc/sudoers

baik, setelah proses diatas. maka anda sudah berhasil melakukan Instalasi Archl Linux di mesin anda.  

