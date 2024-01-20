# Documenation

This documenation is built with sphinx.


#### Make a new conda environment 
* It requires a new conda environment (that is different from the project's environment) with the packages specified in ```skinnet/environment_docs.yaml```

```yaml
# this is a file to make an environment for the documentation of skinnet project
name: skinnet-docs
channels:
  - conda-forge
dependencies:
  - sphinx
  - furo
  - myst-parser
  - sphinx-togglebutton
```

* Make and activate the environment:
```bash
conda env create -f environment_docs.yaml
```
```bash
conda activate skinnet-docs
```


#### Sketch the documentation structure

Following instructions on https://www.sphinx-doc.org/en/master/tutorial/getting-started.html, 
* Having activated the environment, got to the project's root directory (e.g. ```skinnet``` in this case) and run 
```bash
sphinx-quickstart docs
```

* Once prompted, select "separate source and build directories" and answer other questions
* At the end, you will be presented with this filestructure

```
skinnet
└── docs
    ├── build
    ├── make.bat
    ├── Makefile
    └── source
        ├── conf.py
        ├── index.rst
        ├── _static
        └── _templates
```

* ```docs/source/index.rst``` is the root document of the project, which serves as welcome page and contains the root of the “table of contents tree” (or toctree). 

* Whenever you create a new file (page) to your project, add it to the Contents section undet the toctree. For example, for the current file, ```documentation.md```, add the following

```

Contents
--------

.. toctree::

   documentation

```


#### Configure documentation

Customize the documentation using ```conf.py``` file. Example:

```python
# Configuration file for the Sphinx documentation builder.
#
# For the full list of built-in configuration values, see the documentation:
# https://www.sphinx-doc.org/en/master/usage/configuration.html

# -- Project information -----------------------------------------------------
# https://www.sphinx-doc.org/en/master/usage/configuration.html#project-information

project = 'skinnet'
copyright = '2024, pavel kliuiev'
author = 'pavel kliuiev'
release = '1.0.0'


# -- General configuration ---------------------------------------------------
# https://www.sphinx-doc.org/en/master/usage/configuration.html#general-configuration

# simply add the extension to your list of extensions
# myst_parser is needed to integrate markdown with sphinx
# sphinx_togglebutton is to add collapsible content to your documentation
extensions = ['myst_parser', "sphinx_togglebutton"]

# specify valid source files extensions to use for docs - both markdown and RST
source_suffix = {
    '.rst': 'restructuredtext',
    '.md': 'markdown',
}

# The master toctree document.
master_doc = 'index'

templates_path = ['_templates']
exclude_patterns = []


# -- Options for HTML output -------------------------------------------------
# https://www.sphinx-doc.org/en/master/usage/configuration.html#options-for-html-output

# The theme to use for HTML and HTML Help pages.  See the documentation for
# a list of builtin themes.
import furo
html_theme = 'furo'

html_static_path = ['_static']
```


#### Build documentation
Given you are in the project folder containing the ```docs``` folder, run the build:

```bash
sphinx-build -M html docs/source/ docs/build/
```

Now it is ready under ```skinnet/docs/build/html/documentation.html```. 

