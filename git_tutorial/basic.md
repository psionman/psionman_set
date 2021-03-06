---
    layout: page
    title:  ""
---

[Git commands]({{ site.baseurl }}{% link git_tutorial/index.md %})

### Git Basic Commands

1. *init*
    ```bash
    git init
    ```
creates a *.git* directory (a *repository*) in the *working directory* and makes git functionality available.

1. *clone*
    ```bash
    git clone <url of website>
    ```
creates a directory with the same name as the repo and downloads from the *remote origin* all of the files in the repo.

1. *status*
    ```bash
    git status
    ```
displays information about files that have been modified.

    Before any modifications:
    >On branch master
    >
    >Your branch is up-to-date with 'origin/master'.
    >
    >nothing to commit, working tree clean

1. *branch*
    ```bash
    git branch branch_01
    ```
    This creates a *reference* or *checkpoint*. (*commit*s are a special sort of *reverence* of *checkpoint* called a *revision*.)

[Git commands]({{ site.baseurl }}{% link git_tutorial/index.md %})

### Link an existing project with a respository on bitbucket

1. In the terminal
    ```
    git init
    ```

2 . Copy the *git remote add  ...* code and run in terminal

3. In terminal
    ```
    git push --set-upstream origin master
    ```
