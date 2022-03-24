---
title: How to use Poetry to manage dependencies in Python 
date: 2022-03-23 00:00
description: Learn how Poetry can be initialized in a project and used to resolve dependencies.
tags: Python, Basics
path: python-poetry-tutorial
author: Pratik Choudhari
---

The Python programming language has tools for managing environment and interpreter versions such as venv and pyenv respectively. We have talked about virtual environments in Python and how to use them in this [blog post](https://www.python-engineer.com/posts/virtual-environments-python/).

Languages like Node.js, Go and Rust have their own utility CLI tool for helping with environment and dependency management for a project. Python lacks a default tool that can do dependency management hence third-party tools need to be used, one such tool is [poetry](https://python-poetry.org).

In this article, you 
will get an overview of how poetry works and how to manage dependencies in poetry.

## Poetry Installation

Linux/Mac/bashonwindows users should execute the following command in a terminal:

```console
curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py | python -
```

For windows powershell users:

```console
(Invoke-WebRequest -Uri https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py -UseBasicParsing).Content | python -
```

To verify if poetry is successfully installed, open a new terminal and check for the version of poetry:

```console
poetry –version
```

## Creating a Poetry project

To create a new poetry initialized project, we use the command

```console
poetry new my-poetry-project
```

Executing this command will create a folder with the following tree structure

```console
my-poetry-project
├── my_poetry_project
│   └── __init__.py
├── pyproject.toml
├── README.rst
└── tests
    ├── __init__.py
    └── test_my_poetry_project.py
```

If a project is already created, use `poetry init` to initialize poetry.

By default, poetry creates a python package with an appropriate name. The file `pyproject.toml` is used by poetry to keep a track of project info, python version, development dependencies and other externally installed packages. It is worth noting that the dependencies of dependencies is not stored in `pyproject.toml` file.

In Node.js a `package-lock.json` file is created to lock the dependency versions during installation similarly, a `poetry.lock` file is created by poetry to lock dependency versions. Storing the version of every package helps poetry to resolve dependency conflicts while installing/updating packages. Also, when another user will use poetry to install dependency the exact same packages would be downloaded and installed.

## Manage virtual environments with Poetry

One of the core features of poetry is the usage of the virtual environment to isolate the project runtime from the global python runtime. If a user is using poetry inside a virtual environment then poetry keeps using it else it creates a separate virtual environment for the project with the default python version of the computer.

**List available environments**:

```console
poetry env list
```

**Create/use an environment**:

Specify Python version for environment creation/use. Users can use the path to an environments python interpreter.

```console
poetry env use 3.6
```

**Remove an environment**:

```console
poetry env remove env-name
```

## Add packages with Poetry

When a new package is installed both, `pyproject.toml` and `poetry.lock`, are updated. Installation is done using the `poetry add package-name` command, users can also specify version constraints such as:

- `poetry add pendulum@^2.0.5`
- `poetry add "pendulum>=2.0.5"`
- `poetry add pendulum==2.0.5`

To install multiple packages, specify package names in a sequence such as

```console
poetry add pandas numpy matplotlib 
```

## Remove packages with Poetry

Removing package from the project is easy. Whenever a package is removed its unused dependencies are removed too, updating  `pyproject.toml` and `poetry.lock`. To remove multiple packages, specify package names in a sequence.

```console
poetry remove pandas
```

## Update packages with Poetry

Similar to removing a package, updating a package updates `pyproject.toml` and `poetry.lock` with new versions and updated dependencies. To update multiple packages, specify package names in a sequence.

```console
poetry update pandas
```

## Install all project dependencies with Poetry

To setup a newly cloned project with poetry initialized, use the following command

```console
poetry install
```

If `poetry.lock` file is not available, poetry will read the `pyproject.toml` file, resolve the dependencies, install the packages and create lock file. 

If `poetry.lock` file is available, poetry will read from lock file to ensure same package versions are installed as other users.
