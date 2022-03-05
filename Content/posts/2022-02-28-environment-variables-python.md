---
title: How to access and set environment variables in Python
date: 2022-03-06 00:00
description: Learn how environment variables can be retrieved and created using Python.
tags: Python, Basics
path: environment-variables-python
author: Pratik Choudhari
---

Environment variables are stored at the operating system level as key-value pairs, they play a crucial role in abstracting sensitive information.

They also help a programmer in configuring an application just by changing their values instead of hard coding them.

This article will take you through the process of retrieving and setting environment variable values using Python.

## Get environment variable values

The `os` standard library in Python helps in executing tasks at the OS level. We can retrieve environment variables using the following code snippet.

```python
import os

# print all environment variables as a dictionary
print(os.environ)

# get LANG variable without KeyError
print(os.environ.get("LANG"))
```

## Set environment variable

Setting environment variables is the same as setting a key-value pair in a dictionary. Key and value both must be of string data type.

```python
import os

os.environ["MY_CUSTOM_KEY"] = "secret_value"
```
