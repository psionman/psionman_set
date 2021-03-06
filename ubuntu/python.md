---
layout: page
title: ""
---

[Reinstall Ubuntu]({{ site.baseurl }}{% link ubuntu/index.md %})

### Python

1. To set Python 3 as the default:
    ```bash
    sudo update-alternatives --install /usr/bin/python python /usr/bin/python2.7 10
    sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.6 20
    ```
    (The higher number becomes the default.)

1. Install *pip*

    ```bash
    sudo apt-get install python3-pip
    sudo apt install python-pip
    ```

### wxPython

```bash
sudo apt install make gcc libgtk-3-dev libwebkitgtk-dev libwebkitgtk-3.0-dev libgstreamer-gl1.0-0 freeglut3 freeglut3-dev python-gst-1.0 python3-gst-1.0 libglib2.0-dev ubuntu-restricted-extras libgstreamer-plugins-base1.0-dev

pip3 install wxpython
```
(Go and make a cup of coffee!)

<!-- 1. wxPython
    ```bash
    pip3 install wxPython
    ```
    (takes 30+ minutes)

    If this fails with
    > No package ‘gtk+-3.0’ found

    then run
    ```bash
    sudo apt-get install libgtk-3-dev
    ```
    If it fails with
    > No such file or directory: 'build/lib.linux-x86_64-3.6/wx/libwx_baseu-3.0.so'

    ```bash
    sudo apt-get update
    sudo apt-get install libwxgtk3.0-0v5
    ```
    installed *libwxbase3.0-dev* using *Synaptic* -->

1. Python packages to add

    ```bash
    pip install -U pytest
    pip install termcolor
    pip install mock
    pip install PyDispatcher
    pip install python-docx
    pip install PyPDF4
    pip install openpyxl
    ```

1. Setup *virtualenvwrapper*, see [these instructions]({{ site.baseurl }}{% link utilities/virtualenv.md %})

1. Remove *.pyc* etc., see [these instructions]({{ site.baseurl }}{% link utilities/remove_pyc.md %})

[Reinstall Ubuntu]({{ site.baseurl }}{% link ubuntu/index.md %})
