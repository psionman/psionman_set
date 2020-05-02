---
    layout: page
    title:  ""
---

## Sphinx

[Sphinx](https://www.sphinx-doc.org/en/master/usage/quickstart.html) is a a documentation builder that creates html documents from Restructured text.

#### Installing Sphinx

1. Install
    ```console
    pip install -U Sphinx
    ```

1. To use markdown with Sphinx
    ```console
    sudo pip install recommonmark
    ```

#### Start a Sphinx project

1. Navigate to your *docs* directory and enter:
    ```console
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
    source_parsers = {
       '.md': 'recommonmark.parser.CommonMarkParser',
    }
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
