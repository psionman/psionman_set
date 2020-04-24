---
layout: page
title: ""
---

[Reinstall Ubuntu]({{ site.baseurl }}{% link ubuntu/index.md %})

### Add radio stations to RhythmBox

1. https://www.bbc.co.uk/sounds/play/live:bbc_radio_three

1. https://www.bbc.co.uk/sounds/play/live:bbc_radio_fourfm

1. Install extra codecs
  ```console
  sudo apt install ubuntu-restricted-extras
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

[Reinstall Ubuntu]({{ site.baseurl }}{% link ubuntu/index.md %})
