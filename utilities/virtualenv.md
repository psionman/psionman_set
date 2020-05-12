---
    layout: page
    title:  ""
---

## Virtualenv

[Virtualenv](https://virtualenv.pypa.io/en/latest/)  is a utility that enables the user to create and use a separate environment for one or more python projects. Using *virtualenv* in its raw state can lead to a slightly chaotic system with lots of environments in *random* locations. [virtualenvwrapper](https://pypi.org/project/virtualenvwrapper/) addresses this objection in an elegant way.

#### Installing Virtualenv

```bash
python -m pip install --user virtualenv
```

#### Installing VirtualEnvWrapper

```bash
pip install virtualenvwrapper
export WORKON_HOME=~/Envs
mkdir -p $WORKON_HOME
source /usr/local/bin/virtualenvwrapper.sh
```
or
```bash
source ~/.local/bin/virtualenvwrapper.sh
```
depending on the location of *virtualenvwrapper.sh*.

If necessary, add the following  lines to *~/.bashrc*

```
export WORKON_HOME=~/Envs
source /usr/local/bin/virtualenvwrapper.sh
```


This will set up the *Envs* directory as the home for all of you virtualenvs.

#### Creating a new VirtualEnv

```bash
mkvirtualenv <env name>
```

#### To list VirtualEnvs
```bash
workon
```

#### To activate a VirtualEnv
```bash
workon <env name>
```

#### Site packages
To toggle access to site packages (e.g. wxPython):
```bash
toggleglobalsitepackages
```
