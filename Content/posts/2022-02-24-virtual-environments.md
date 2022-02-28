---
title: What are virtual environments in Python and how to work with them
date: 2022-03-01 00:00
description: Understand why virtual environments are required and how to manage them.
tags: Python, Basics
path: virtual-environments-python
author: Pratik Choudhari
---

Python has robust support for third-party libraries. Instead of writing code themselves, users can install already built solutions using `pip` (a package management tool for Python). Although this ability to easily integrate foreign packages gives Python a superpower, managing the packages and their versions can quickly turn into a mess.

Using virtual environments users can manage libraries without conflicting with other installations. In this article, we will dive deeper into using `venv` for virtual environment management in Python.

## What are virtual environments?

Every Python installation creates root site-directories, which means there is always one environment that can be used system-wide. Different projects have different requirements and therefore using the root Python installation will lead to frequent Install/Uninstall of packages. This creates a lot of friction while working and wastes time and effort.

![Virtual environments](/images/2022-01-29-virtual-environments/venv.webp)

Virtual environments aim to isolate the Python execution and the dependency environment from the root environment. Using this tool users can use different environments for different projects with zero conflicts. There can be different versions of a package installed in two different virtual environments.

[`venv`](https://docs.python.org/3/library/venv.html) is a standard Python package that is used to create virtual environments.

## How does `venv` work?

Every virtual environment has its own Python binary which is a copy of the Python version used during creation. A `pyvenv.cfg` file is created in the environment directory specifying information about the environment such as the path to Python which was used for creation, its version, and whether packages installed in system Python are copied.

On virtual environment activation, `venv` prepends the path to the virtual environment binary, like */home/user/Desktop/my\_env/bin/*,  to the `PATH` system variable. When a script is executed it refers to the virtual environment Python binary files rather than system Python binaries.

## Working with virtual environments

### Creation

The following command is used to create a virtual environment:

```console
$ python3 -m venv /path/to/new/virtual/environment
```

For example, using the following will create a virtual environment with the name **venv** in the current working directory:

```console
$ python3 -m venv venv
```

### Activation

Depending on your specific OS and shell type, commands can slightly differ. A full list with all activation commands can be found [here](https://docs.python.org/3/library/venv.html).

The two most common commands for macOS/Linux and Windows are listed below. Replace **\<venv\>** with the path to virtual environment:

#### macOS/Linux:

```console
$ . <venv>/bin/activate
```

or

```console
$ source <venv>/bin/activate
```

#### Windows:

```console
$ <venv>\Scripts\activate.bat
```

### Deactivation

A virtual environment can be deactivated, irrespective of OS and shell type, using the following command

```console
$ deactivate
```

### Deletion

To delete a virtual environment simply delete the virtual environment folder. Either manually or in the console, e.g.:

```console
$ rm -rf venv
```
