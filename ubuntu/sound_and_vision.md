---
layout: page
title: ""
---

[Reinstall Ubuntu]({{ site.baseurl }}{% link ubuntu/index.md %})

### Shortwave Radio

1. Install [*Flatpack*](https://flatpak.org/setup/Ubuntu/)
    ```bash
    sudo add-apt-repository ppa:alexlarsson/flatpak
    sudo apt update
    sudo apt install flatpak
    sudo apt install gnome-software-plugin-flatpak
    flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
    ```
1. Install [Shortwave](http://ubuntuhandbook.org/index.php/2020/03/internet-radio-player-shortwave-1-0-released/)
```bash
flatpak install flathub de.haeckerfelix.Shortwave
```
Terminal command to run shortwave:
```bash
flatpak run de.haeckerfelix.Shortwave  
```

### Install OpenShot

1. In terminal:
  ```bash
  sudo add-apt-repository ppa:openshot.developers/ppa
  sudo apt-get update
  sudo apt-get install openshot-qt
  ```

### Install Audacious

1. In terminal:
  ```bash
  sudo apt-get install audacious
  ```

### Install SM Player

1. In terminal:
  ```bash
  sudo add-apt-repository ppa:rvm/smplayer
  sudo apt-get update
  sudo apt-get install smplayer smplayer-themes smplayer-skins
  ```

1. To update the toolbar:

   1. Make sure SmPlayer is closed

   1. edit *~/.config/smplayer/smplayer.ini*
     ```bash  
     [mini_gui]
     actions\controlwidget=play_or_pause, stop, separator, timeslider_action, separator, fullscreen, mute, volumeslider_action, repeat, set_a_marker, clear_ab_markers, set_b_marker
     ```

### Spotify
```bash
snap install spotify
```

### pulseaudio

If *pulseaudio* does not start, add the following command to *Startup Applications*
```bash
pulseaudio --start
```


### Serviio

1. Download instructions are on the [Wiki page](https://wiki.serviio.org/doku.php?id=howto:linux:install:ubuntu18-04).
This is a summary.

1. In the Terminal
    ```bash
    sudo apt update
    sudo apt upgrade
    sudo apt install net-tools software-properties-common openjdk-8-jre default-jre ffmpeg dcraw wget
    cd /opt
    sudo wget http://download.serviio.org/releases/serviio-2.0-linux.tar.gz
    sudo tar zxvf serviio-2.0-linux.tar.gz
    sudo ln -s serviio-2.0 serviio
    sudo chown -R root:root /opt
    ```

1. Start the server
    ```bash
    sudo /opt/serviio/bin/serviio.sh
    ```
1. Check in the browser at [http://192.168.1.138:23423/bash](http://192.168.1.138:23423/bash) (use *ifconfig* to get ip address)

1. If it's working
    ```bash
    sudo rm serviio-2.0-linux.tar.gz
    ```
1. Create *serviio.service*
    ```bash
    sudo gedit /lib/systemd/system/serviio.service
    ```
    Paste in the following:
    ```
    [Unit]
    Description=Serviio Media Server
    After=syslog.target local-fs.target network.target

    [Service]
    Type=simple
    ExecStart=/opt/serviio/bin/serviio.sh
    ExecStop=/opt/serviio/bin/serviio.sh -stop
    KillMode=none
    Restart=on-abort

    [Install]
    WantedBy=multi-user.target
    ```
1. Enable the Service
    ```bash
    sudo systemctl daemon-reload
    sudo systemctl enable serviio.service
    sudo systemctl start serviio.service
    ```
1. Reboot the system

### OBS Studio

```bash
udo apt install ffmpeg
sudo add-apt-repository ppa:obsproject/obs-studio
sudo apt update
sudo apt install obs-studio
```

### Add radio stations to RhythmBox

  (N.B. Not official BBC urls)

 1. http://bbcmedia.ic.llnwd.net/stream/bbcmedia_radio3_mf_p

 1. http://bbcmedia.ic.llnwd.net/stream/bbcmedia_radio4fm_mf_p

 1. Install extra codecs (f necessary)
   ```bash
   sudo apt install ubuntu-restricted-extras
   ```

[Reinstall Ubuntu]({{ site.baseurl }}{% link ubuntu/index.md %})
