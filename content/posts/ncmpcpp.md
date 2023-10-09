---
title: "configuring ncmpcpp and mpd"
date: 2023-08-05T20:00:20+03:00
description: 'ncmpcpp, a terminal based music player for mpd| configuring ncmpcpp'
tags: "cli-based software,"
tags: "music"
image: images/ncmpcpp
draft: false
---

### mpd client

MPD is free & open music player server. That is, rather than being a full
fledged music player it only operates in the background and we can interact
with it using it's client to do every a music player does like create
playlists, shuffle through playlist, access to visualizers, tag editors, among
other things.

In my opinion ncmpcpp is the best of these clients and I will be covering how
to install and configure it on linux.

### ncmpcpp

Ncmpcpp is a terminal based music player meaning we use it in the command line
and most navigation will be done using your keyboard as opposed to using the
mouse as you do in your traditional GUI applications. 

### Features
 - Ncmpcpp comes with a rich set of features making it a viable alternative to 
   your favourite GUI music player
 - these features include:
   - tag editor
   - playlist editor
   - easy to use search engine
   - media library
   - music visualizer
   - ability to fetch artist info from last.fm
   - new display mode
   - alternative user interface
   - ability to browse and add files from outside of MPD music directory …and 
    a lot more minor functions.
   - and also with a fair bit of hacking ability to play your spotify playlists
   
   
In this article I will show you how to configure ncmpcpp. To run ncmpcpp you should
first run mpd with the command 
```bash
   $ mpd
```
and then run ncmpcpp with
```bash
    $ ncmpcpp
```

### Configuring Ncmpcpp
 1. First we start by configuring the mpd.conf which should be located in the
    below file path \
    <span style="color:yellow"> <b> ~/home/usr/.config/mpd/mpd.conf </b> </span>
 - you can copy the default configuration from with the command
  ```bash
  $ cp /etc/mpd/mpd.conf $HOME/.config/mpd/mpd.conf
   ```
   OR
   ```bash
   $ cp /etc/mpd/mpd.conf $HOME/.mpd/mpd.conf
   ```
    
 - the configurations are in plain-text making it extremely easy to understand
   </br> as you can see in the image below. 
   <img src="/images/mpdconfig.png" width="cover" alt="my mpd configuration file">

2. Now to the ncmpcpp config file which should be located in <span
style="color:yellow"> <b> ~/home/usr/.config/ncmpcpp/config </b> </span> \
the default configuration 

   <img src="/images/ncmpcppconfig.png" width="cover" alt="ncmpcpp configuration file">

There are way more options than the one's you see in the above picture of the 
ncmpcpp configuration file above.

The default config file comes with all options commented out meaning they are in
default state. You change options by uncommenting them and then giving a valid 
alternative.

1. Let's go through each of the configurations in the image above.
 - **ncmpcpp_directory** sets the folder location for your configurations. In my
 case this is *~/.config/ncmpcpp*
 - **lyrics_directory** ncmpcpp has support downloading & viewing lyrics. this
 option sets where the lyrics will be downloaded and search for.
 - **lyrics_fetchers** this sets where ncmpcpp will fetch lyrics from. Priority
 will be set from left to right. In our case ncmpcpp will first search musixmatch
 followed by genius, & finally azlyrics. 
 
     **Note: I have found musixmatch to be the most reliable hence why I have 
     set it to have the highest priority**
 - **store_lyrics_in_song_dir** I have set this to no as that would coz a mess.    
 - **mpd_music_dir** this sets where mpd will search for your music files. It is 
   best practice to store your music files in *~/Music*
 - **execute_on_song_change** this is used to execute certain commands whenever
 a song changes. In this case, I have set it to show a popup notification with
 the herbe program displaying the now playing song information.

That's all I will cover here. For more comprehensive information on ncmpcpp visit
[it's archwiki entry](https://wiki.archlinux.org/title/Ncmpcpp).
