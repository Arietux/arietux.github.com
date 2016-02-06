---
layout: post
title: Cara backup system linux dengan rsync
description: backup system linux menggunakan aplikasi rsync
keywords: archlinux, backup, linux, restore, rsync
---

Banyak berbagai macam cara backup system linux contohnya seperti cloning menggunakan clonezilla ataupun dd. Namun system cloning tersebut tidak flexibel, artinya sistem kloning yang di lakukan clonezilla dan dd yaitu membackup seluruh block dalam partisi, hal ini tentu tidak efisien. _Kenapa tidak efisien ?_ misalkan linux anda terinstal di sebuah partisi dengan ukuran partisi 50GB, sedangkan sistem linux anda hanya berukuran 15GB, tentunya anda rugi 25GB dalam menyimpan hasil backup nanti :)

Nah, dengan menggunakan rsync. Sitem backup jadi lebih flexibel karena mirip seperti menyalin file menggunakan perintah **cp** namun **rsync** jauh lebih baik lagi dalam hal ini.

### Catatan

* Saya sudah coba sendiri pada distro Arch Linux dan Ubuntu yang saya miliki
* Cermatilah setiap langkah tutorial dibawah dengan teliti, DWYOR!
* **Silahkan tanya pada kolom komentar dibawah jika ada yang anda tidak mengerti atau ada yang ingin ditanyakan mengenai artikel ini.**
* Bagi yang memiliki partisi penyimpanan data selain di direktori **home** maka harus di masukkan ke opsi **–exclude**. dalam contoh saya, saya memiliki partisi yang khusus dibuat untuk menyimpan data data ( musik,dokumen,video,dll ) pada partisi** /dev/sda8** yang di mount pada direktori **/data**. Hal ini guna untuk memisahkan proses backup data system linux anda dengan data personal anda.
* Sudah itu saja.
* Ada lagi ?

### Persiapan

* Sediakan harddisk eksternal dengan filesystem linux (ext3,ext4,dll) tentunya harus lebih besar dari system linux yang akan anda backup.
* Sediakan Live CD linux ( pastikan live cd linux yang anda miliki sudah memiliki aplikasi rsync )

### Backup

Instal terlebih dahulu aplikasi rsync di linux anda Kemudian jalankan perintah dibawah ini  

    rsync -aAXv \--exclude={"/dev/*","/proc/*","/sys/*","/tmp/*","/run/*","/mnt/*","/media/*","/lost+found"} /* /letak/partisi/ekternal/backup

  
**Penting:**  
– Jika anda memiliki partisi internal yang termount otomatis saat start ( **fstab** ) pastikan untuk menambahkan partisi yang berhubungan dengan penyimpanan data eksternal di masukkan ke dalam opsi **exclude** diatas. sebagai contoh saya memiliki partisi **/dev/sda8** yang di mount ke direktori **/data** sebagai partisi khusus data seperti ( musik,file,video,dll ). 
– Jika anda menggunakan **swapfile ** pastikan anda masukkan pada opsi exclude.  
– Jika anda ingin membackup partisi `/home` pastikan beberapa path ini `/home/*/.thumbnails/*`, `/home/*/.cache/mozilla/*`, `/home/*/.cache/chromium/*`, `/home/*/.local/share/Trash/*`, `/home/*/.gvfs` dimasukkan ke dalam opsi exclude.
3. tunggulah proses backup hingga selesai, lama waktu backup tergantung dengan besar system linux dan kondisi harddisk yang anda miliki.

### Restore

**Persiapan :**

Siapkan terlebih dahulu partisi backup dan partisi untuk restore sistem linux anda, sebagai contoh liat daftar partisi yang saya miliki :

  

| Nama      | Mount point |
| --------- | ----------- |
| /dev/sda6 | /           |
| /dev/sda1 | /boot       |
| /dev/sda7 | /var        |
| /dev/sda5 | linux swap  |

**Mount partisi :**

    mkdir /mnt/restore
    mount /dev/sda6 /mnt/restore
    mkdir /mnt/restore/{boot,var}
    mount /dev/sda1 /mnt/restore/boot
    mount /dev/sda7 /mnt/restore/var
    swapon -p 0 /dev/sda5

**Restore backup :**

sebagai contoh, hdd eksternal yang saya gunakan berada di /dev/sdb3

    mkdir /mnt/hddeksternal
    mount /dev/sdb3 /mnt/hddeksternal
    rsync -aAXv /mnt/hddeksternal/backup/* /mnt/restore

nah kemudian silahkan tunggu prosesnya hingga selesai 😀

**Langkah Akhir (CHROOT) :**

Ingat, ini adalah lanjutan dari langkah sebelumnya. di langkah terakhir ini saya split menjadi 2 bagian yaitu Arch Linux dan Ubuntu.

Arch Linux :

    genfstab -p -U /mnt &gt; /mnt/restore/etc/fstab
    arch-chroot /mnt/restore /bin/bash
    grub-install \--target=i386-pc \--recheck \--debug /dev/sda
    cp /usr/share/locale/en@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo
    grub-mkconfig -o /boot/grub/grub.cfg
    mkinitcpio -p linux
    exit
    umount /mnt/restore/{boot,var}
    umount /mnt/restore
    reboot

Ubuntu :

Sayangnya ubuntu masih belum memiliki tool untuk membuat fstab secara otomatis dari partisi yang di mount sebelumnya ( arch linux menggunakan genfstab ), jadi disini kita akan melakukannya secara manual .

berdasarkan partisi yang saya gunakan, maka seperti ini lah bentuk **fstab** nya :

    # <file system=""> <mount point=""> <type> <options> <dump> <pass>
    
    proc /proc proc nodev,noexec,nosuid 0 0
    
    #/dev/sda6 root
    
    UUID=3fc55e0f-a9b3-4229-9e76-ca95b4825a40 / ext4 rw,errors=remount-ro 0 1
    
    #/dev/sda5 swap
    
    UUID=718e611d-b8a3-4f02-a0cc-b3025d8db54d none swap sw 0 0
    
    #/dev/sda1 boot
    
    UUID=41e60bc2-2c9c-4104-9649-6b513919df4a /boot ext4 defaults 0 2
    
    #/dev/sda7
    
    UUID=02fc2eda-d9fb-47fb-9e60-5fe3073e5b55 /var reiserfs rw,noatime,nodiratime,notail 0 0


Simpan fstab tersebut di **/mnt/restore/etc/fstab** silahkan di sesuaikan fstab diatas dengan partisi yang anda gunakan. untuk melihat **UUID** bisa menggunakan perintah **blkid**. kemudian jalankan perintah dibawah :

    cd /mnt/restore/
    mount -t proc proc proc/
    mount \--rbind /sys sys/
    mount \--rbind /dev dev/
    chroot /mnt/restore /bin/bash
    export PS1="(chroot) $PS1"
    update-grub
    /usr/sbin/grub-install \--recheck \--no-floppy /dev/sda
    sync
    exit
    umount /mnt/restore/{boot,var}
    umount /mnt/restore
    reboot

Maka selesai lah proses **backup** dan **restore** sistem linux yang anda miliki. 😀

Maka saya akhiri artikel ini. semoga berguna buat anda kelak, saya mohon maaf jika ada kata yang tidak berkenan di hati anda baik di sengaja maupun tak sengaja.

Terimakasih.

Referensi :  
https://wiki.archlinux.org/index.php/Full_system_backup_with_rsync  
https://help.ubuntu.com/community/BackupYourSystem%20  
http://askubuntu.com/questions/81726/how-to-rebuild-fstab-automatically

