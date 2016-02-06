---
layout: post
title: pemutar musik mpd dan ncmpcpp
description: konfigurasi mpd dan ncmpcpp di archlinux
keywords: ncmpcpp, mpd, archlinux, musik
---

_Ncmpcpp _ atau  _NCurses Music Player Client Plus Plus_ adalah pemutar musik klien yang sangat di gandrungi oleh kaum pemuda masa kini. Banyak anak muda yang menggunakan pemutar musik ini dengan alasan ringan dan minimalis dan biar "_Kekinian". _Tak sedikit pula orang orang yang kadang salah saat dalam menyebutkan aplikasi ini, "_Ncpmcpcm" "Npmcppc" _dan lain sebagainya.

Untuk menjalankan musik dari aplikasi Ncmpcpp, perlu diketahui bahwa kita harus mengkonfigurasi Music Player Daemon atau disingkat MPD terlebih dahulu. Berikut proses instalasi dan konfigurasinya.

#### Installasi :

    sudo pacman -S ncmpcpp mpd mpc

#### Konfigurasi :

**MPD :**  

1\. Memasukan mpd ke grub audio

    $ sudo gpasswd -a mpd audio

2\. Membuat file konfigurasi

    $ mkdir -p ~/.mpd/playlists
    $ touch ~/.mpd/{mpd.conf,database,log,pid,state,sticker.sql}

3\. konfigurasi file mpd.conf

    music_directory    "/dataku/Musik" # Disesuaikan dengan musik direktori agan
    playlist_directory "~/.mpd/playlists"
    db_file            "~/.mpd/database"
    log_file           "~/.mpd/log"
    pid_file           "~/.mpd/pid"
    state_file         "~/.mpd/state"
    sticker_file       "~/.mpd/sticker.sql"
    
    audio_output {
            type                    "fifo"
            name                   "my_fifo"
            path                     "/tmp/mpd.fifo"
            format                 "44100:16:2"
    
    #Audio Output
    #kalau pake pulseaudio, konfigurasi Alsanya di beri tanda pagar ( Comment ) begitu juga sebaliknya
    
    #Pulseaudio
    audio_output {
      type    "pulse"
      name    "pulse audio"
    }
    
    #Alsa
    audio_output {
            type         "alsa"
            name         "My Sound Card"
            mixer_type   "software"      # optional
    }

4\. Selesai tinggal simpan.

**Ncmpcpp :**

1\. buat file konfigurasi  

    mkdir ~/.ncmpcpp
    nano ~/.ncmpcpp/config


2\. Konfigurasi ncmpcpp

    mpd_music_dir = "/dataku/Musik" # disamakan folder musiknya dengan konfigurasi mpd tadi.
    /* mpd */
    mpd_crossfade_time = "3"
    
    /* UI */
    song_list_format = " {$2%a$1 - }{$8%t$1}$R{$1%l} "
    song_status_format = "$2%a $1:: $4%t $1:: $3%b$1"
    song_columns_list_format = "(8f)[black]{l}  (32)[red]{a} (42)[yellow]{t|f} (18)[magenta]{b}"
    now_playing_prefix = ""
    now_playing_suffix = "$/b"
    selected_item_prefix = "$3"
    selected_item_suffix = "$9"
    progressbar_look = "░█ "
    alternative_header_first_line_format ="{$b$2%a$9} $1::$9 {$5%t$9}"
    alternative_header_second_line_format ="{$6%b$9} $1::$9 {$2(%y)$9}"
    user_interface = "classic"
    browser_display_mode = "columns"
    header_visibility = "no"
    statusbar_visibility = "yes"
    titles_visibility = "no"
    mouse_support = "no"
    fancy_scrolling = "yes"
    cyclic_scrolling = "yes"
    autocenter_mode = "yes"
    centered_cursor = "yes"
    discard_colors_if_item_is_selected = "no"
    display_remaining_time = "yes"
    display_bitrate = "no"
    playlist_disable_highlight_delay = "1"
    playlist_display_mode = "classic"
    enable_window_title = "no"
    clock_display_seconds = "no"
    
    /* colors */
    colors_enabled = "yes"
    statusbar_color = "black"
    empty_tag_color = "yellow"
    main_window_color = "black"
    main_window_highlight_color = "black"
    volume_color = "black"
    color1 = "white"
    color2 = "blue"
    progressbar_color = "black"
    statusbar_color = "black"
    active_column_color = "red"
    window_border_color = "red"
    active_window_border = "red"
    header_window_color = "black"
    alternative_ui_separator_color ="black"
    
    /* visualizer */
    visualizer_fifo_path = "/tmp/mpd.fifo"
    visualizer_output_name = "Visualizer"
    visualizer_type = "wave" (spectrum/wave)
    visualizer_sync_interval = "30"
    visualizer_color = "red"
    visualizer_in_stereo = "yes"

setelah itu simpan.

**Let's Play :**

Jalankan perintah **mpd** pada terminal, oh iya, setelah jalankan mpd lalu jalankan perintah **mpc update** untuk mengupdate database musiknya.

![][1]

kalau udah ada kata-kata succeeded, tandanya udah berhasil sekarang jalankan perintah **ncmpcpp** di terminal.

![][2]

wah !! kok kosong ?  Pasti gagal nih, gagal nih, gatot nih !! 
tenang gan :D, itu menu playlist kok, memang pertama-tamanya kosong dulu karena belum ada musik yang dimainkan. coba sekarang tekan tombol 3, ntar muncul deh daftar musiknya. tinggal pencet tombol **enter** untuk memainkan musiknya. terus tekan tombol 2 lagi untuk masuk ke playlist 😀

berikut kumpulan screenshot ncmpcpp nya :

![][3]


![][4]


![][5]


![][6]

Referensi :  
https://wiki.archlinux.org/index.php/ncmpcpp#Different_views  
http://dotshare.it/category/mpd/ncmpcpp/

[1]: http://www.kawainaaa.com/wp-content/uploads/2014/08/Screenshot-2Bfrom-2B2014-08-15-2B10-3A25-3A23.png
[2]: http://www.kawainaaa.com/wp-content/uploads/2014/08/Screenshot-2Bfrom-2B2014-08-15-2B10-3A33-3A48.png
[3]: http://www.kawainaaa.com/wp-content/uploads/2014/08/Screenshot-2Bfrom-2B2014-08-15-2B10-3A41-3A10.png
[4]: http://www.kawainaaa.com/wp-content/uploads/2014/08/Screenshot-2Bfrom-2B2014-08-15-2B10-3A42-3A37.png
[5]: http://www.kawainaaa.com/wp-content/uploads/2014/08/Screenshot-2Bfrom-2B2014-08-15-2B10-3A42-3A50.png
[6]: http://www.kawainaaa.com/wp-content/uploads/2014/08/Screenshot-2Bfrom-2B2014-08-15-2B10-3A43-3A04.png