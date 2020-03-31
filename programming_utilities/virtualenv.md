---
    layout: page
    title:  ""
---

## Virtualenv

[Virtualenv](https://virtualenv.pypa.io/en/latest/)  is a utility that enables the user to create and use a separate environment for one or more python projects. Using *virtualenv* in its raw state can lead to a slightly chaotic system with lots of environments in *random* locations. [virtualenvwrapper](https://pypi.org/project/virtualenvwrapper/) addresses this objection in an elegant way.

#### Installing Virtualenv

```console
python -m pip install --user virtualenv
```

#### Installing VirtualEnvWrapper

```console
pip install virtualenvwrapper
export WORKON_HOME=~/Envs
mkdir -p $WORKON_HOME
source /usr/local/bin/virtualenvwrapper.sh
```

This will set up the *Envs* directory as the home for all of you virtualenvs.

#### Creating a new VirtualEnv

```console
mkvirtualenv django
```

#### To list VirtualEnvs
```console
workon
```

#### To activate a VirtualEnv
```console
workon django
```
