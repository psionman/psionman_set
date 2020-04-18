---
layout: page
title: ""
---

[Build Ubuntu]({{ site.baseurl }}{% link ubuntu/index.md %})

### Install Jekyll

(https://psionman.github.io/psionman_set)

1. In terminal

    ``` console
    sudo apt-get install ruby-full build-essential zlib1g-dev
    echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
    echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
    echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
    source ~/.bashrc
    gem install jekyll bundler
    ```
    (Takes some time!)

1. If necessary:
    ``` console
    bundle install
    ```

### Install Atom

1. Go to the [Download site](https://atom.io/)

1. Download the *.deb* file

1. Open with *Software Install*

1. Change theme in *Edit/Preferences/Themes*

1. To install tool-bar
   ```console
   apm install tool-bar
   apm install tool-bar-atom
   ```
1. To toggle menu bar in Atom press the *Alt* key.


[Build Ubuntu]({{ site.baseurl }}{% link ubuntu/index.md %})
