---
layout: page
title: ""
---

[Reinstall Ubuntu]({{ site.baseurl }}{% link ubuntu/index.md %})

### Dropbox

1. In terminal
  ```bash
  cd ~ && wget -O - "https://www.dropbox.com/download?plat=lnx.x86_64" | tar xzf -
  ~/.dropbox-dist/dropboxd
  ```

1. Add Dropbox command to *Preferences/Startup Applications* in main Ubuntu menu:
  ```bash
  /home/jeff/.dropbox-dist/dropboxd
  ```
  (Not sure this works)

 1. This does. in */etc/init.d/* create a file *dropbox* and populate with:
    ```bash
    #!/bin/sh
    ### BEGIN INIT INFO
    # Provides:          dropbox
    # Required-Start:    $remote_fs $syslog
    # Required-Stop:     $remote_fs $syslog
    # Should-Start:      $network $time $local_fs
    # Should-Stop:       $network $time $local_fs
    # Default-Start:     2 3 4 5
    # Default-Stop:      0 1 6
    # Short-Description: dropbox - file synchronization daemon
    # Description:       Dropbox is a Web-based file hosting service operated by
    #                    Dropbox, Inc. that uses cloud storage to enable users to store and share files
    #                    and folders with others across the Internet using file synchronization
    ### END INIT INFO

    DROPBOX_USERS="dropbox"

    DAEMON=.dropbox-dist/dropboxd

    # dropbox shouldn't try to connect to X server
    unset DISPLAY

    start() {
        echo "Starting dropbox..."
        for dbuser in $DROPBOX_USERS; do
            HOMEDIR=`getent passwd $dbuser | cut -d: -f6`
            if [ ! -f $HOMEDIR/.dropbox/info.json ]; then
                echo "$dbuser is not linked to a dropbox account yet.  Cannot start dropbox."
                continue
            fi
            if [ -x $HOMEDIR/$DAEMON ]; then
                HOME="$HOMEDIR" start-stop-daemon -b -o -c $dbuser -S -u $dbuser -x $HOMEDIR/$DAEMON
            fi
        done
    }

    stop() {
        echo "Stopping dropbox..."
        for dbuser in $DROPBOX_USERS; do
            HOMEDIR=`getent passwd $dbuser | cut -d: -f6`
            if [ -x $HOMEDIR/$DAEMON ]; then
                start-stop-daemon -o -c $dbuser -K -u $dbuser -x `/bin/ls -1 $HOMEDIR/.dropbox-dist/dropbox-lnx.*/dropbox`
            fi
        done
    }

    status() {
        for dbuser in $DROPBOX_USERS; do
            dbpid=`pgrep -u $dbuser dropbox`
            if [ -z $dbpid ] ; then
                echo "dropboxd for USER $dbuser: not running."
                exit 1
            else
                echo "dropboxd for USER $dbuser: running (pid $dbpid)"
                exit 0
            fi
        done
    }

    case "$1" in

        start)
            start
            ;;

        stop)
            stop
            ;;

        restart|reload|force-reload)
            stop
            start
            ;;

        status)
            status
            ;;

        *)
            echo "Usage: /etc/init.d/dropbox {start|stop|reload|force-reload|restart|status}"
            exit 1

    esac

    exit 0
    ```

[Reinstall Ubuntu]({{ site.baseurl }}{% link ubuntu/index.md %})
