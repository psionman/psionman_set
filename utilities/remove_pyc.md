---
    layout: page
    title:  ""
---

## Remove and disable pyc files and folders

#### To remove existing pyc files and directories
```console
find . | grep -E "(__pycache__|\.pyc|\.pyo$)" | xargs rm -rf
export PYTHONDONTWRITEBYTECODE=1
source ~/.bashrc
```
