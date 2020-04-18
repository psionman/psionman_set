---
    layout: page
    title:  ""
---


### Terminal commands

1. To see list of recent commands:
    ```console
    history 25
    ```

1. To search for a command in recent commands:
    ```console
    <CTRL>R
    Type in the start of the command
    ```

### To list a program's dependencies
E.g for *rhythmbox*
```console
apt-cache depends rhythmbox
```

### To check that a lib is installed
E.g for *libgstreamer-plugins-base1.0-0*
```console
ldconfig -p | grep libgstreamer-plugins-base1.0-0
```
If it exists you will see a list of information, if not, nothing is output.
