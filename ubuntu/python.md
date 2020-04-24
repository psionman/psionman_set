---
layout: page
title: ""
---

[Build Ubuntu]({{ site.baseurl }}{% link ubuntu/index.md %})

### Python

1. To set Python 3 as the default:
    ```console
    sudo update-alternatives --install /usr/bin/python python /usr/bin/python2.7 10
    sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.6 20
    ```
    (The higher number becomes the default.)

1. Install *pip*

    ```console
    sudo apt-get install python3-pip
    sudo apt install python-pip
    ```

1. wxPython
    ```console
    pip3 install wxPython
    ```
    (takes 30+ minutes)

    If this fails with
    > No package ‘gtk+-3.0’ found

    then run
    ```console
    sudo apt-get install libgtk-3-dev
    ```
    If it fails with
    > No such file or directory: 'build/lib.linux-x86_64-3.6/wx/libwx_baseu-3.0.so'

    ```console
    sudo apt-get update
    sudo apt-get install libwxgtk3.0-0v5
    ```

1. Python packages to add

    ```console
    pip install -U pytest
    pip install termcolor
    pip install mock
    ```

1. Setup *virtualenvwrapper*, see [these instructions]({{ site.baseurl }}{% link programming_utilities/virtualenv.md %})

1. Remove *.pyc* etc., see [these instructions]({{ site.baseurl }}{% link programming_utilities/remove_pyc.md %})

[Build Ubuntu]({{ site.baseurl }}{% link ubuntu/index.md %})
