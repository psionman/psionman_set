---
layout: page
title: ""
---

[Reinstall Ubuntu]({{ site.baseurl }}{% link ubuntu/index.md %})

### Miscellaneous

1. Add *.scripts* to PATH:
    ```bash
    export PATH="$HOME/.scripts:$PATH"
    ```

1. Add folder to Caja favourites
  Edit *.config/user-dirs.dirs*

    or

    Enter directory and click on *Bookmark*

1. Install Synaptic (if missing):
    ```bash
    sudo apt-get install synaptic apt-xapian-index
    sudo update-apt-xapian-index -vf
    ```

1. Add the EN-GB dictionary
    ```bash
    sudo apt install hunspell-en-gb
    ```

1. If *open in terminal* is missing from Caja:
    ``` bash
    sudo apt-get install caja-open-terminal
    ```
    (Log out if necessary to install)

1. Sphinx
    ```bash
    pip install Sphinx
    pip install sphinx_rtd_theme
    ```

1. Tree
    ```
    sudo apt install tree
    ```

1. If LaTeX is missing
    ```bash
    sudo apt-get install texlive-latex-recommended texlive-latex-extra texlive-fonts-recommended

    ```
    install latexmk from [this download page](https://packages.ubuntu.com/xenial/all/latexmk/download)


1. Install [PrintFriendly](https://www.printfriendly.com/) to Firefox.

[Build Ubuntu]({{ site.baseurl }}{% link ubuntu/index.md %})
