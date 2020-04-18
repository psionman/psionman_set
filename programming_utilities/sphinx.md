---
    layout: page
    title:  ""
---

## Sphinx

[Sphinx](https://www.sphinx-doc.org/en/master/usage/quickstart.html) is a a documentation builder that creates html documents from Restructured text.

#### Installing Sphinx

```console
pip install -U Sphinx
```
#### Start a Sphinx projects

Navigate to your *docs* directory and enter:
```console
sphinx-quickstart
```
Sphinx will then run through the questions it needs a to create the project.

To use the ReadTheDocs theme, in *conf.py* in your source directory:
```python3
html_theme = "sphinx_rtd_theme"
```

#### To use markdown with Sphinx

```console
sudo pip install recommonmark
```

In *conf.py*

```python3
source_suffix = ['.rst', '.md']
source_parsers = {
   '.md': 'recommonmark.parser.CommonMarkParser',
}
```
