---
    layout: page
    title:  ""
---

## Sphinx

[Sphinx](https://www.sphinx-doc.org/en/master/usage/quickstart.html) is a a documentation builder that creates html documents from Restructured text.

#### Installing Sphinx

1. Install
    ```bash
    pip install -U Sphinx
    ```

1. To use markdown with Sphinx
    ```bash
    sudo pip install recommonmark
    ```

#### Start a Sphinx project

1. Navigate to your *docs* directory and enter:
    ```bash
    sphinx-quickstart
    ```
    Sphinx will then run through the questions it needs a to create the project.


1. To use the *ReadTheDocs* theme, in *conf.py* in your source directory:

    ```python3
    html_theme = "sphinx_rtd_theme"
    ```
1. To use *markdown*
    ```python3
    source_suffix = ['.rst', '.md']
    source_parsers = {'.md': 'recommonmark.parser.CommonMarkParser',}
    ```

1. To remove blank pages from LaTeX documents: in *conf.py*:

    ```python3
    latex_elements = { 'classoptions': ',openany,oneside'}
    ```

#### To use figure numbers

1. Add the following to *conf.py*:

    ```python3
    numfig = True
    ```

1. A figure element should look like:

    ```python3
    .. figure:: /images/simple_modern_acol.png
       :scale: 30
       :alt: Convention Card
       :figclass: align-center
       :name: simple_modern_acol

       Convention Card
    ```
1. Any reference to the figure should take the form:

    ```python3
    (See :numref:`simple_modern_acol` A sample convention card)
    ```

### To use markdown

See [Sphinx pages](https://www.sphinx-doc.org/en/master/usage/markdown.html)

1. In terminal
    ```
    pip install --upgrade recommonmark
    ```
2. in conf.py
    ```python3
    from recommonmark.parser import CommonMarkParser
    ...
    extensions = ['recommonmark']
    ...
    source_parsers = {'.md': 'recommonmark.parser.CommonMarkParser',}
    source_suffix = {
        '.rst': 'restructuredtext',
        '.txt': 'markdown',
        '.md': 'markdown',
    }
    ```
