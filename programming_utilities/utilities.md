---
    layout: page
    title:  ""
---

## Make utility available system wide

### Python

1. Find the location of your *site-packages* directory
    ```console
    python -m site --user-site
    ```
which will display a site, say *\<site-packages>*

1. Place the module in a directory in

    > \<site-packages>

1.Create a bash script in *~/.scripts* e.g.

    ```console
    #!/bin/bash
    python <site-packages><module>/main.py
    ```
