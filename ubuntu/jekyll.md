---
layout: page
title: ""
---

[Reinstall Ubuntu]({{ site.baseurl }}{% link ubuntu/index.md %})

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

1. *Watchers*
   ```console
   echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p
   ```

[Reinstall Ubuntu]({{ site.baseurl }}{% link ubuntu/index.md %})
