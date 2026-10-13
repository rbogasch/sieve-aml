# Minimal makefile for Sphinx documentation
.DEFAULT_GOAL := help

SPHINXOPTS    ?=
VENV_PYTHON  := $(abspath ../.venv/bin/python)
PYTHON       ?= python3
SPHINXBUILD  ?= $(VENV_PYTHON) -m sphinx
SOURCEDIR     = .
BUILDDIR      = _build

.PHONY: help Makefile clean html linkcheck doxygen setup-python

setup-python:
	$(PYTHON) -I -c 'import sys; sys.exit(0 if sys.version_info[:2] == (3, 14) else "Python 3.14 is required")'
	$(PYTHON) -I -m venv ../.venv
	$(VENV_PYTHON) -m pip install --upgrade pip
	$(VENV_PYTHON) -m pip install -r requirements.txt
	$(VENV_PYTHON) -m pip check

help:
	@$(SPHINXBUILD) -M help "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)

clean:
	rm -rf $(BUILDDIR)
	rm -rf ../doxygen

doxygen:
	cd .. && doxygen Doxyfile

html: doxygen
	@$(SPHINXBUILD) -M html "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)

html-no-doxygen:
	@$(SPHINXBUILD) -M html "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)

linkcheck:
	@$(SPHINXBUILD) -M linkcheck "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)

# Catch-all target
%: Makefile
	@$(SPHINXBUILD) -M $@ "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)
