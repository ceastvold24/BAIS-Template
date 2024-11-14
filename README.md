# BAIS-Template

### To Do List

---

[x] task 1  
[ ] task 2  
~[ ] task 3~

### Change Log

---

- 11/13/2024 name added file
- 11/13/2024 name changed title

### Jupyter Notebook Code Quality

nbQA:
Installation

pip install nbqa

Confirmation:

nbqa --version

You will get a version response if it installed correctly.

nbstripout:
Install in your base environment

pip install nbstripout

Confirmation:

nbstripout --version

You will get a version response if it installed correctly.

Install in you repository:

nbstripout --install

This must be done each time you create a repository.

Usage:

nbstripout your_notebook.ipynb

isort:
Installation

pip install isort

Confirmation:

isort --version

You will get a version response if it installed correctly.

Usage:

nbqa isort your_notebook.ipynb

Black:
Installation

pip install black

Confirmation:

black --version

You will get a version response if it installed correctly.

Usage:

nbqa black your_notebook.ipynb

Flake8:
Installation

pip install flake8

Confirmation:

flake8 --version

You will get a version response if it installed correctly.

Usage:

nbqa flake8 your_notebook.ipynb

Bandit: (doesn't work on notebooks, only .py scripts)
Installation

pip install bandit

Confirmation:

bandit --version

You will get a version response if it installed correctly.

Usage:

nbqa bandit your_notebook.ipynb

Run all tests on all Notebooks (.ipynb):
nbqa nbstripout .

nbqa isort .

nbqa black .

nbqa flake8 .

Pre-commit Hook:
In each repository

pre-commit install

nbstripout --install

.pre-commit-config.yaml in the root of your repository

exclude: '\.ipynb_checkpoints/' # don't check files in this directory

repos:

- repo: https://github.com/kynan/nbstripout
  rev: 0.5.0
  hooks:

  - id: nbstripout
    name: nbstripout (clear notebook output)

- repo: https://github.com/nbQA-dev/nbQA
  rev: 1.5.2 # Latest stable version of nbQA
  hooks:

  - id: nbqa-isort
    name: isort (nbqa)
    args: ["--profile=black"]
    additional_dependencies: ["isort", "setuptools"]

  - id: nbqa-black
    name: black (nbqa)
    args: ["--line-length=88"] # Black’s default line length
    additional_dependencies: ["black==23.9.1", "setuptools"] # Ensure Black and setuptools are available

  - id: nbqa-flake8
    name: flake8 (nbqa)
    args:
    - --max-line-length=88
    - --ignore=E203,W503
      additional_dependencies: ["flake8", "setuptools"]
