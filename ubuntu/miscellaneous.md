---
layout: page
title: ""
---

[Build Ubuntu]({{ site.baseurl }}{% link ubuntu/index.md %})

### Miscellaneous

1. Add folder to Caja favourites
  Edit *.config/user-dirs.dirs*

    or

    Enter directory and click on *Bookmark*

1. Install Synaptic (if missing):
    ```console
    sudo apt-get install synaptic apt-xapian-index
    sudo update-apt-xapian-index -vf
    ```

1. Add the EN-GB dictionary
    ```console
    sudo apt install hunspell-en-gb
    ```

1. If *open in terminal* is missing from Caja:
    ``` console
    sudo apt-get install caja-open-terminal
    ```
    (Log out if necessary to install)

1. Sphinx
    ```console
    pip install Sphinx
    pip install sphinx_rtd_theme
    ```

1. If LaTeX is missing
    ```console
    sudo apt-get install texlive-latex-recommended texlive-latex-extra texlive-fonts-recommended

    ```
    install latexmk from [this download page](https://packages.ubuntu.com/xenial/all/latexmk/download)

[Build Ubuntu]({{ site.baseurl }}{% link ubuntu/index.md %})
