---
title: How to work with ZIP files in Python
date: 2022-04-30 00:00
description: Learn ZIP file manipulation with the zipfile module.
tags: Python, Basics
path: python-zip
author: Pratik Choudhari
---

ZIP format is commonly used as a file archival as well as compression format which is supported across all platforms. Files can be compressed without losing any data. Python has built-in support for ZIP files.

In this article, we will learn how ZIP files can be read, written, extracted, and listed in Python.
 
## List ZIP file contents
 
The [zipfile](https://docs.python.org/3/library/zipfile.html) module in Python, a part of the built-in libraries, can be used to manipulate ZIP files. It is advised to work with file handlers inside a context manager as it takes care of file pointer closure.
 
To read a ZIP file we first create an instance of the `ZipFile` class and use the following methods to get file information:
 
```python
import zipfile
 
with zipfile.ZipFile("./data.zip") as zip:
    print("As table:")
    print(zip.printdir()) # display files and folders in tabular format
    print("\nAs list:")
    print(zip.namelist()) # list of files and folders
    print("\nAs list of objects:")
    print(zip.infolist()) # get files as ZipInfo objects
```
 
Output:
 
```console
As table:
File Name                                    Modified                       Size
data/                                        2022-04-24 19:00:16            0
data/assets/                                 2022-04-24 19:00:24            0
data/assets/index.txt                        2022-04-24 19:01:12           11
data/configurations.txt                      2022-04-24 18:52:26            0
data/sample.txt                              2022-04-24 18:52:16            0

As list:
['data/', 'data/assets/', 'data/assets/index.txt', 'data/configurations.txt', 'data/sample.txt']

As list of objects:
[<ZipInfo filename='data/' external_attr=0x10>, <ZipInfo filename='data/assets/' external_attr=0x10>, <ZipInfo filename='data/assets/index.txt' compress_type=deflate external_attr=0x20 file_size=11 compress_size=13>, <ZipInfo filename='data/configurations.txt' external_attr=0x20 file_size=0>, <ZipInfo filename='data/sample.txt' external_attr=0x20 file_size=0>]
```
 
## Read specific files from ZIP

After a ZIP file is read, use the `open()` method to read a specific file.
 
```python
import zipfile
 
with zipfile.ZipFile("./data.zip") as zip:
    with zip.open("data/assets/index.txt") as fp:
        print(fp.read().decode())
```
 
Output:
 
```console
hello-world
```
 
## Adding files to a ZIP

To add files we first open the ZIP file in append mode. It is **important not to open it in write mode** because then the entire ZIP will be overwritten!

```python
import zipfile

with zipfile.ZipFile("./data.zip", "a") as zip:
    zip.write("app.py", arcname="python/app.py")
```
Here, `arcname` is used to define the path of file inside the ZIP. 

## Extracting the contents

Extraction is pretty simple. For this the file needs to be opened in read mode:

```python
import zipfile

with zipfile.ZipFile("./data.zip", "a") as zip:
    zip.extractall() # extract data into current working directory
```

Extracting password protected ZIP:

```python
import zipfile

with zipfile.ZipFile("./data.zip", "a") as zip:
    zip.extractall(pwd=bytes(pswd, 'utf-8'))
```

