---
layout: post
title: Alasan anda harus menggunakan Tiling WM di linux.
description: alasan mengapa anda harus menggunakan tiling wm
keywords: archlinux, linux, opini, xmonad
---

Pernahkah sebelumnya anda mendengar kata **Tiling WM** ? Tiling WM ( Window Manager ) adalah sebutan untuk **Window Manager** yang dapat menyusun jendela aplikasi agar tidak saling tumpang tindih. Jendela yang saling timpang tindih sangatlah tidak efisien jika anda membutuhkan beberapa aplikasi lain untuk tampil bersamaan dengan aplikasi yang sedang anda kerjakan guna memudahkan pekerjaan anda.

Misalnya anda sebagai pengguna desktop environtmen biasa ( Kde, Xfce, Gnome, Unity,dll)  saat anda ingin membuat sebuah program aplikasi, tentunya aplikasi yang akan anda buka adalah text editor ( sebagai media untuk menulis skrip pemrograman anda ) dan browser ( sebagai media untuk mencari referensi mengenai pemrograman yang akan anda buat). Dari permisalan tersebut, berikut beberapa hal yang dilakukan oleh kebanyakan pengguna dalam menggunakan text editor dan broser dalam keperluan tadi, yaitu :

1\. Anda hanya menampilkan text editor secara penuh ( maximize ) di layar desktop anda. Dan saat anda membutuhkan referensi dari internet, anda harus mengeklik browser di panel anda atau menekan tombol  kombinasi keyboard alt+tab untuk membuka browser guna untuk melihat referensi. Hal tersebut tidak efisien karena anda harus bolak balik pindah aplikasi antara text editor dan browser.

<img src="{{ site.baseurl }}/images/2015/08/Screenshot_2015-08-26_19-21-41.png" alt="preview" style="width: 600px;"/>

2\. Anda akan menampilkan browser secara penuh lalu menampilkan text editor. Nah disini lah terjadinya aksi tumpang tindih antar jendela, tentunya untuk melihat referensi sekaligus menggunakan text editor, maka akan menyesuaikan ukuran jendela text editor anda agar referensi yang anda buka dari browser kelihatan. Hal ini tidak efisien, selain karena sebagian artikel tertutup oleh text editor, ukuran jendela text editor yang relatif kecil membuat anda sedikit tidak nyaman dalam membuat program.

<img src="{{ site.baseurl }}/images/2015/08/Screenshot_2015-08-26_19-22-17.png" alt="preview" style="width: 600px;"/>

3\. Anda akan mengatur jendela browser dan text editor ke dalam 2 bagian untuk mempermudah dalam membuat program. cukup efisien tapi ribet, karena dalam point ini anda harus mengatur ukuran jendela aplikasi menggunakan mouse dengan manual. Yup, *"anda harus menggunakan mouse dan mengarahkan pointer ke sisi jendela lalu mendrag ke sisi lain untuk mengatur ukuran jendela sesuai dengan yang anda kehendaki"*. Okelah, kalau untuk mengukur 2 jendela aplikasi setengah layar anda, anda bisa mengatur tanpa harus ribet mengarahkan pointer ke sisi jendela, cukup dengan mendrag jendela aplikasi ke pinggir layar desktop anda, maka ukuran jendela aplikasi akan otomatis memenuhi setengah layar anda. Tapi bagaimana jika anda ingin mengatur ukuran jendela aplikasi lebih lebar dari pada jendela browser ? bagai mana jika aplikasi yang anda buka lebih dari 2 ? maka dengan terpaksa anda harus mengatur ukuran jendela aplikasi tersebut secara menual satu per satu, ehmm.. ehmm.. saya ulangi, **Satu per satu !** 

<img src="{{ site.baseurl }}/images/2015/08/Screenshot_2015-08-26_19-29-47.png" alt="preview" style="width: 600px;"/>

Dari 3 point diatas, ***efisien*** lebih merujuk pada penghematan waktu dan tenaga. *"Ah masnya lebay banget deh, beberapa detik kebuang untuk geser jendela aplikasi ga masalah mah"*. Ya untuk sebagian orang hal ini mungkin akan di anggap lebay, tapi bagi orang yang menganut paham "***Waktu adalah uang***" maka hal ini sangat lah penting walaupun hanya **1 detik**.

"*Terus yang lebay itu pasti soal penghematan tenaga, geser geser mouse ga bakal bikin mas lemes kok mas*". Tidak juga sih setiap anggota tubuh yang bergerak itu tentu membutuhkan tenaga hehehe. sebenernya "penghematan tenaga" hanya alias saja, di pake untuk menggantikan kata "malas", yup malas menggunakan tangan untuk menggerakkan mouse, kelihatan sepele ya ? tapi ini soal menghemat waktu "_malas membuang waktu_" . Saya juga percaya, terciptanya sebuah **Tiling WM** juga berasal dari orang malas. Bahkan **malas** dapat memunculkan sesuatu yang positif seperti **menghemat waktu**. Dengan ini saya percaya dengan quote mas Bill Gates, yaitu :

> "I choose a lazy person to do a hard job. Because a lazy person will
> find an easy way to do it."

Selain soal _efisiensi,_ ada lagi keuntungan yang dapat anda ambil dari sebuah **Tiling WM** yaitu borderless ( tidak ada border ) ini akan membuat layar anda tampak semakin luas, apalagi jika anda hanya mempunyai resolusi layar yang kecil misalnya 1024×800, inti dari Borderless yaitu _**Hemat ruang Layar**_.

<img src="{{ site.baseurl }}/images/2015/08/Screenshot_2015-08-26_21-22-32.png" alt="preview" style="width: 600px;"/>

**Tidak Hanya Itu!** masih banyak lagi keuntungan yang akan anda dapatkan saat menggunakan **Tiling WM** selain efisiensi dan borderless, yaitu :

####Mouseless :
Definisi Mouseless disini yaitu anda tidak perlu menggunakan mouse dalam semua aktifitas menyangkut tentang Jendela Aplikasi, semua bisa di lakukan dengan menggunakan Keyboard. berikut contoh video menggeser, mengubah ukuran, serta mengganti fokus pada Jendela Aplikasi **Tiling WM**.

  
####Hemat Penggunaan CPU dan Memory :
Bagi anda yang memiliki spesifikasi cpu dan memory RAM yang rendah, tiling wm akan berjalan cepat serta pemakaian cpu dan ram yang rendah.

<img src="{{ site.baseurl }}/images/2015/08/Screenshot_2015-08-26_21-35-17.png" alt="preview" style="width: 600px;"/>

penggunaan cpu dan ram pada tiling wm xmonad

Tiling WM juga bukan hanya **Xmonad**, masih banyak lagi Tiling WM selain Xmonad, yaitu :

* Awesome
* Bspwm
* DWM
* i3
* SubtleWM
* Qtile
* MonsterWm
* Dll.

Demikianlah penjelasan dan opini dari saya mengenai "Alasan kenapa anda harus menggunakan Tiling WM", semoga tulisan saya ini dapat berguna bagi anda. Saya mohon maaf jika ada yang tidak berkenan di hati anda atas tulisan saya baik secara sengaja maupun tidak sengaja dalam tulisan saya.

Terimakasih.