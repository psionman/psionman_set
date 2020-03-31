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

2. Place the module in a directory in


> \<site-packages>

2. Create a bash script e.g.

```console
#!/bin/bash
python <site-packages><module>/main.py
```
in

> ~/.scripts
