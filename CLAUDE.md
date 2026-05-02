# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is the Sphinx documentation site for the [Courtois NeuroMod](https://www.cneuromod.ca/) project — a large longitudinal neuroimaging dataset (6 subjects, ~200h fMRI/subject). Published at [docs.cneuromod.ca](https://docs.cneuromod.ca/en/latest/) and auto-deployed from the `main` branch via ReadTheDocs.

## Build

```bash
pip install -r requirements.txt   # sphinx, sphinx-rtd-theme, myst-parser
make html                          # outputs to build/html/
```

For a clean build (required when changing the table of contents):
```bash
rm -rf build/ && make html
```

Note: `requirements.txt` is managed by git-annex (a symlink). Run `datalad get requirements.txt` if the file is not populated.

## Architecture

- `source/conf.py` — Sphinx config: uses `myst_parser` (for `.md` files) and `sphinx.ext.autosectionlabel`; theme is `sphinx_rtd_theme`.
- `source/index.rst` — top-level table of contents. **New pages must be explicitly listed here** (or in a nested `toctree`) to appear in the docs.
- `source/OVERVIEW.rst` — landing page content, included via `.. include::` in `index.rst`.
- `source/*.md` — main documentation sections (ACCESS, MRI, DATASETS, DERIVATIVES, RELEASES, CONTRIBUTING, AUTHORS, ACKNOWLEDGMENT).
- `source/datasets/` — sub-section for individual dataset pages (`hcptrt_bids.md`, `anat.md`); controlled by `source/datasets/index_bids.rst`.
- `source/img/` — images referenced as `img/filename.png` in docs.
- `source/_static/` — PDFs, BibTeX, and other linked assets.
- `source/datasets/cneuromod.all` — DataLad/git-annex submodule with per-dataset BIDS metadata. Initialize with `datalad get -n -r source/datasets/cneuromod.all/*/bids && datalad update -r --merge`.

## Adding content

To add a new top-level page, create `source/MYPAGE.md` and add `MYPAGE` (no extension) to the `toctree` in `source/index.rst`.

To add a new dataset page, create `source/datasets/mydata.md` and add `mydata` to the `toctree` in `source/datasets/index_bids.rst`.

Markdown files support MyST syntax including admonition blocks (`::: {important}`, `::: {tip}`) via the `colon_fence` extension.
