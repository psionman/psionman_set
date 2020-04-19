---
    layout: page
    title:  ""
---

## Remove and disable pyc files and folders

#### To remove existing pyc files and directories
```console
find . \( -name "*__pycache__" -o -name "*.pyc" -o -name "*.pyo" \) -delete
export PYTHONDONTWRITEBYTECODE=1
source ~/.bashrc
```
