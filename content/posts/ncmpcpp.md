---
sitemap:
    changefreq: hourly
    priority: 0.8
title: "how to configure & install ncmpcpp on linux"
date: 2023-08-05T20:00:20+03:00
description: 'ncmpcpp is a terminal based music player, this is a guide showing how to configure ncmpcpp'
tags: "music"
image: images/ncmpcpp
draft: false
---

# Introduction
- ncmpcpp is a frontend for Music Player Daemon (MPD). MPD is a music player 
  server that plays and organises audio files, playlists, etc.
- to interact (in a user friendly manner) with MPD we need a client application
and ncmpcpp is one of these application.
- ncmpcpp is a fork of ncmpc that comes with many more features including but not
limited to visualizer, tag editor, playlist editor, lyrics display and download.
- ncmpcpp is a terminal based application

## how to install ncmpcpp
- ncmpcpp is available on most linux distribution repositories. In my case I use
**Fedora Linux** so I use the following command;
```bash
sudo dnf5 install mpd ncmpcpp
``` 
for Debian-based 'ubuntu, linux mint, etc' distros;
```bash
sudo apt-get install mpd ncmpcpp
```
## configuring MPD
- we will create a configuration file in **.config/mpd/mpd.conf**, this file 
will override the default system-wide configuration.
```bash
touch .config/mpd/mpd.conf
```
- you can also use **.mpd/mpd.conf** 
```bash
touch .mpd/mpd.conf
```

here is my configuration file;
```bash
   1   | music_directory     "/home/user/Music"
   2   │ playlist_directory  "/home/user/.config/mpd/playlists"
   3   │ 
   4   │ auto_update "yes"
   5   │ bind_to_address "127.0.0.1"
   6   │ restore_paused "yes"
   7   │ max_output_buffer_size "16384"
   8   │ 
   9   │ audio_output {
  10   │     type "pulse"
  11   │     name "pulse"
  12   │     #type  "alsa"
  13   │     #name  "ALSA"
  14   │ }
  15   │ 
  16   │ audio_output {
  17   │        type "fifo"
  18   │        name "Visualizer feed"
  19   │        path "/tmp/mpd.fifo"
  20   │        format   "44100:16:2"
  21   │ }
```
Replace ***user*** with your username

In the **audio_output** option I have set *type* and *name* to pulse because I am 
using pulseaudio as my output source. you can switch to alsa instead.

---
**NOTE:** There are many more options than this & you can explore them in **/etc/mpd.conf** \
You will also find explanations for each option in the same file. 
**DO NOT MAKE DIRECT CHANGES TO THIS FILE UNLESS YOU KNOW WHAT YOU ARE DOING**

---

## configuring ncmpcpp
- we will create a configuration file in **.config/ncmpcpp/config**, this file 

```bash
vim .config/ncmpcpp/config
```

- now we add the configuration content
```bash
   1   │ ncmpcpp_directory = ~/.config/ncmpcpp
   2   │ lyrics_directory = ~/.lyrics
   3   │ mpd_music_dir = ~/Music
   4   │ mpd_crossfade_time = 12
   5   │ visualizer_look = ^|
   6   │ visualizer_spectrum_smooth_look = no 
   7   │ execute_on_song_change = herbe "Now Playing" "$(mpc --format '%title% \n%artist% - %album%' current)" 
   8   │ playlist_display_mode = columns
   9   │ browser_display_mode = columns
  10   │ search_engine_display_mode = columns
  11   │ playlist_editor_display_mode = columns
  12   │ progressbar_look = **
  13   │ user_interface = alternative
  14   │ media_library_albums_split_by_date = no
  15   │ statusbar_visibility = no
  16   │ connected_message_on_startup = no
  17   │ lyrics_fetchers = musixmatch, genius, azlyrics
  18   │ fetch_lyrics_for_current_song_in_background = yes
  19   │ store_lyrics_in_song_dir = no 
  20   │ screen_switcher_mode = playlist, browser, lyrics
  21   │ startup_screen = playlist
  22   │ jump_to_now_playing_song_at_start = yes
  23   │ display_bitrate = yes
  24   │ external_editor = nvim
  25   │ header_window_color = default
  26   │ color2 = green
```

---
**NOTE:** for *execute_on_song_change* you will need to download herbe 
```bash
sudo dnf5 install herbe
```
---

## Startup 
First we start mpd
```bash
mpd
```
Then we start ncmpcpp
```bash
ncmpcpp
```

## Lets explore ncmpcpp
### this is the playlist screen
<figure>
<img src="/images/ncmpcpp_current_playlist" width="cover" alt="ncmpcpp playlist screen">
<figcation>Fig.1 - ncmpcpp playlist view</figcation>
</figure>

On startup of ncmcpp you will be greeted by the current playlist display. To navigate 
here from other areas use Press **1**

Press **u** to update the database so your audio files are visible to ncmpcpp

### media library
<figure>
<img src="/images/ncmpcpp_media_lib" width="cover" alt="ncmpcpp playlist screen">
<figcation>Fig.2 - ncmpcpp media library</figcation>
</figure>

This is the ncmpcpp media library. Press **4** to navigate to this screen.
As you can see in Fig.2 the Albums are sorted by artist, to sort by date press
**4** again

### lyrics view
<figure>
<img src="/images/ncmpcpp_lyrics" width="cover" alt="ncmpcpp playlist screen">
<figcation>Fig.2.1 - ncmpcpp lyrics view with lyrics to MF DOOM's "Korn Karne"</figcation>
</figure>

One of the features of ncmpcpp is the ability to download and view lyrics. To switch
to this view press **l** with the selection on the song whose lyrics you want to 
view.

You press **F** to toggle fetching lyrics on song change.


### visualizer
<figure>
<img src="/images/ncmpcpp_visualizer" width="cover" alt="ncmpcpp playlist screen">
<figcation>Fig.2.2 - ncmpcpp visualizer</figcation>
</figure>

Ncmpcpp comes with a visualizer which can be access by pressing **8**. We can configure
its look in the ncmpcpp config.



## Conclusion
There it is that is enough to get you started with ncmpcpp. For more ricing options
you can visit forums such as r/unixporn on reddit, search for ncmpcpp dotfiles
off of github and gitlab.

For a comprehensive list of keybindings visit [ncmpcpp cheatsheet]("https://pkgbuild.com/~jelle/ncmpcpp/")

For more configuration options see the ncmpcpp man pages with 
```bash
man ncmpcpp
```
