---
layout: page
title: ""
---

[Reinstall Ubuntu]({{ site.baseurl }}{% link ubuntu/index.md %})

### Shortwave Radio

1. Install [*Flatpack*](https://flatpak.org/setup/Ubuntu/)
    ```console
    sudo add-apt-repository ppa:alexlarsson/flatpak
    sudo apt update
    sudo apt install flatpak
    sudo apt install gnome-software-plugin-flatpak
    flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
    ```
1. Install [Shortwave](http://ubuntuhandbook.org/index.php/2020/03/internet-radio-player-shortwave-1-0-released/)
```console
flatpak install flathub de.haeckerfelix.Shortwave
```
Terminal command to run shortwave:
```console
flatpak run de.haeckerfelix.Shortwave  
```

### Install OpenShot

1. In terminal:
  ```console
  sudo add-apt-repository ppa:openshot.developers/ppa
  sudo apt-get update
  sudo apt-get install openshot-qt
  ```

### Install Audacious

1. In terminal:
  ```console
  sudo apt-get install audacious
  ```

### Install SM Player

1. In terminal:
  ```console
  sudo add-apt-repository ppa:rvm/smplayer
  sudo apt-get update
  sudo apt-get install smplayer smplayer-themes smplayer-skins
  ```

1. To update the toolbar:

   1. Make sure SmPlayer is closed

   1. edit *~/.config/smplayer/smplayer.ini*
     ```console  
     [mini_gui]
     actions\controlwidget=play_or_pause, stop, separator, timeslider_action, separator, fullscreen, mute, volumeslider_action, repeat, set_a_marker, clear_ab_markers, set_b_marker
     ```

### Add radio stations to RhythmBox

 (N.B. Not official BBC urls)

 1. http://bbcmedia.ic.llnwd.net/stream/bbcmedia_radio3_mf_p

 1. http://bbcmedia.ic.llnwd.net/stream/bbcmedia_radio4fm_mf_p

 1. Install extra codecs (f necessary)
   ```console
   sudo apt install ubuntu-restricted-extras
   ```

[Reinstall Ubuntu]({{ site.baseurl }}{% link ubuntu/index.md %})
