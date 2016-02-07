---
layout : post
title : Twitteran dari CLI
description : twitteran dari cli biar dikatain hacker
keywords : hacker, twitteran, cli, command line interface, linux
---

Awalnya sih saya mau pake kata `terminal` untuk pengganti kata `cli`, tapi saya kasihan sama yang awam yang ga tau apa itu **`terminal`**, ntar malah dikirain terminal kereta api lagi :laughing:. Untuk yang belum tahu saja, jadi ini saya jelasin. Terminal itu adalah penyebutan untuk Command Line Interface di linux. jadi orang-orang IT kalo nyebut kata terminal pasti itu merujuk ke CoLI (Command Line Interface) nya linux.

Balik ke topik utama, jadi setelah 2 hari ini saya berkutat dengan jekyll dan embel-embelnya saya jadi terbiasa untuk melakukan apa-apa dari terminal, dimulai dari pengeditan artikel menggunakan `nano`, git commit, push, gem install, bundle install, itu saya lakuin dari terminal. 

Nah, permasalahannya muncul saat saya ingin mengajukan pertanyaan yang berkaitan dengan indihome di twitter, karena saya lagi asik-asiknya menggunakan terminal ( sebenarnya udah lama asik, tapi akhir2 ini pake terminal hanya buat update system doang :trollface:) saya search dah di google dengan keyword **`twitter cli`**, dan akhirnya ketemu ini [github.com/sferik/t](https://github.com/sferik/t). Itu tool yang jelas gunanya buat update status di twitter, tapi yang kerennya dari tool ini yaitu :

* unfollow orang yang kita follow tapi ga follow kita
* unfollow beberapa orang yang udah lama ga update status di twitter
* dan lain lain.

sekarang bagi yang tertarik silahkan ikutin step step berikut.

### Install Dependensi

#### Ubuntu varians
```
sudo apt-get update && sudo apt-get install ruby1.9.3
```

#### Archlinux
```
sudo pacman -Sy && sudo pacman -S ruby
```

### Install t (twitter cli)

#### run as normal user
```
gem install t
```

#### configure gem path
isikan baris ini di shell konfigurasi (bashrc/zshrc)
```
export PATH="$PATH:$(ruby -rubygems -e "puts Gem.user_dir")/bin"
```

#### konfig t (twitter cli)
lanjut jalankan script dibawah ini di terminal, kemudian ikutin instruksi yang muncul.
```
t authorize
```

setelah toolnya di autorize, sekarang kamu bisa *Twitteran dari cli* :trollface:. Dan untuk panduan lengkapnya silahkan saja langsung kunjungi [github.com/sferik/t](https://github.com/sferik/t).

#### berikut beberapa screenshot penggunaannya.

*Update Status*

![update status]({{ site.baseurl }}/images/201602/ss1.png)

*check timeline*

![check timeline]({{ site.baseurl }}/images/201602/ss2.png})