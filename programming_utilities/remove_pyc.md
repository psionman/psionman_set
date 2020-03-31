---
    layout: page
    title:  ""
---

## Remove and disable pyc files and folders

#### To remove existing pyc files and directories
```console
find . -name "\*.pyc" -delete
find . \| grep -E "(\_\_pycache__\|\.pyc\|\.pyo$)" \| xargs rm -rf
```

#### To prevent Python from ever writing those files again

Set the environment variable PYTHONDONTWRITEBYTECODE to 1.

You can ensure that that variable is set for any bash session that you start by adding the following to your ./profile (or .bashrc):

```console
export PYTHONDONTWRITEBYTECODE=1
source ~/.bashrc
```
