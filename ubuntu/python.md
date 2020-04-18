---
layout: page
title: ""
---

[Build Ubuntu]({{ site.baseurl }}{% link ubuntu/index.md %})

### Setup Python

To set Python 3 as the default:
```console
sudo update-alternatives --install /usr/bin/python python /usr/bin/python2.7 10
sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.6 20
```
(The higher number becomes the default.)

Install *pip*

```console
sudo apt-get install python3-pip
sudo apt install python-pip
```

Setup *virtualenvwrapper*, see [these instructions]({{ site.baseurl }}{% link programming_utilities/virtualenv.md %})

[Build Ubuntu]({{ site.baseurl }}{% link ubuntu/index.md %})
