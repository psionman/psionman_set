---
layout: page
title: ""
---

[Reinstall Ubuntu]({{ site.baseurl }}{% link ubuntu/index.md %})

### Setup MATE desktop


1. Install gedit on gnome from *Activities*

1. Install MATE

	```console
	sudo add-apt-repository ppa:jonathonf/mate-1.22
	sudo apt update
	sudo apt install mate-desktop-environment
	```
	(Quite slow - lot to do)

1. Logout (or restart first time!)

1. Choose MATE from the login screen

1. Select *Radiance* theme

1. Set background

1. If *open in terminal* is missing from Caja:
``` console
sudo apt-get install caja-open-terminal
```
    (Log out if necessary to install)

1. If *MATE Tweak* is missing from *Control Centre*
```console
sudo add-apt-repository ppa:ubuntu-mate-dev/trusty-mate
sudo apt-get update
sudo apt-get install mate-tweak
```
Use this to remove *Home* folder from desktop.


[Reinstall Ubuntu]({{ site.baseurl }}{% link ubuntu/index.md %})
