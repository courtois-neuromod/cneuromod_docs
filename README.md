# Courtois NeuroMod documentation

This is the technical documentation of the Courtois project on neuronal modelling (Courtois NeuroMod). The most recent version of the docs is published on [docs.cneuromod.ca](http://docs.cneuromod.ca/en/latest/).

The docs are built with [sphinx](http://www.sphinx-doc.org!) Content is mostly composed of markdown files (with a few .rst) located in `source`, and  
the website itself is located in `build`. All `source` changes on the master branch will automatically update the website, through integration with [readthedocs](https://readthedocs.org/). To test updates to the website locally, clone or download this repository, install the dependencies (python3) using:
```
pip install -r requirements.txt
```

and then type
```
make html
```
