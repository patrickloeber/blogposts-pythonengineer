---
title: How to use dotenv package to load environment variables in Python 
date: 2022-04-04 00:00
description: Know how environment variables can be set and used in different setup.
tags: Python, Basics
path: dotenv-python
author: Pratik Choudhari
---

Working with environment variables in Python is easy, getting and setting of variables is done using the `os` standard library, however, what if a user wants to set the environment variables when a program is executed and also avoid version controlling the variable values? The `dotenv` package does exactly that.

In this article, we will see how [dotenv](https://github.com/theskumar/python-dotenv) can be used to load and use environment variables from a file.

## Installation

```console
pip3 install python-dotenv
```

## Storing the values in `.env` file

`dotenv` loads the environment variable by reading them from a `.env` file which needs to be inside the project directory.

The `.env` file has declarations in the form of key-value pairs separated by `=`, following is an example of the contents of a `.env` file.

```console
ACCESS_TOKEN=ABC123
SECRET_TOKEN=SUPERSECRET123
```

Using Multi-line values:

```console
ACCESS_TOKEN=ABC123
SECRET_TOKEN="SUPERSECRET123
CONTINUEDSECRET"
```

OR

```console
ACCESS_TOKEN=ABC123
SECRET_TOKEN="SUPERSECRET12\nCONTINUEDSECRET"
```

A variable's value can be used again in the same file using the `${VAR}` syntax.

```console
ROOT_PATH=home/user
LOGS_PATH=${ROOT_PATH}/logs
```

## Loading `.env` file

### Loading as environment variable

The `dotenv` package provides a `load_dotenv()` method which reads the file provided as a file path. If no path is specified, `./.env` is used as the default path which means it looks for `.env` file in the Python script directory.

```python
from dotenv import load_dotenv

load_dotenv()
```

### Loading as a dictionary

Using this method, environment variables are not affected. Instead, they are parsed and converted into a Python dictionary.

```python
from dotenv import dotenv_values

config = dotenv_values(".env")
print(config)
```

Output:

```console
{'ACCESS_TOKEN': 'ABC123', 'SECRET_TOKEN': 'SUPERSECRET12'}
```

## Versioning environment variables

A project can have multiple instances like testing, development, staging or production. When using different instances different environment variables can be needed. Therefore, to solve this issue, a project can use multiple `.env` files like

- `.env.shared`
- `.env.development`
- `.env.production`

Segregation of variables into different files can allow us to version control environment files.
