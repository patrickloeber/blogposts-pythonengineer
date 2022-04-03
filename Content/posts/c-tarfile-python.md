---
title: How to work with tarball/tar files in Python 
date: 2022-04-03 00:00
description: Learn to manage tar files using the tarfile standard module.
tags: Python, Basics
path: tarfile-python
author: Pratik Choudhari
---

TAR stands for Tape Archive Files and this format is used to bundle a set of files into a single file, this is specifically helpful when archiving older files or sending a bunch of files over the network. The Python programming language has [`tarfile`](https://docs.python.org/3/library/tarfile.html) standard module which can be used to work with tar files with support for gzip, bz2 and lzma compressions.

In this article, we will see how `tarfile` is used to read and write tar files in Python.

## Reading a tar file

The `tarfile.open` function is used to read a tar file, it returns a `tarfile.TarFile` object.

The two most important arguments this function takes are the filename and operation mode, with the former being a path to the tar file and the latter indicating the mode in which the file should be opened.

The operation mode can be optionally be paired with a compression method, the new syntax, therefore, becomes `mode[:compression]`. 

Following are the abbreviations for supported compression techniques:

- `gz` for gzip
- `bz2` for bz2
- `xz` for lzma 

Example:

```python
import tarfile

with tarfile.open("sample.tar", "r") as tf:
    print("Opened tarfile")
```

## Extracting tar file contents

After opening a file, extraction can be done using `tarfile.TarFile.extractall` method. Following are the important arguments accepted by the method:
- path: path to a directory to which a tar file should be extracted, defaults to “.” 
- members: specify files to be extracted, should be a subset of  `tarfile.TarFile.getmembers()` output, by default all files are extracted

Example:

```python
import tarfile

with tarfile.open("sample.tar", "r") as tf:
    print("Opened tarfile")
    tf.extractall(path="./extraction_dir")
    print("All files extracted")
```

### Extracting single file

In order to selectively extract files, we need to pass a reference of the file object or file path as string to `tarfile.TarFile.extract` method. To list all files inside a tar file use the `tarfile.TarFile.getmembers` method which returns a list `tarfile.TarInfo` class instances.

Example:

```python
import tarfile

with tarfile.open("./sample.tar", "r") as tf:
    print("Opened tarfile")
    print(tf.getmembers())
    print("Members listed")
```

Output:

```console
Opened tarfile
[<TarInfo 'sample' at 0x7fe14b53a048>, <TarInfo 'sample/sample_txt1.txt' at 0x7fe14b53a110>, <TarInfo 'sample/sample_txt2.txt' at 0x7fe14b53a1d8>, <TarInfo 'sample/sample_txt3.txt' at 0x7fe14b53a2a0>, <TarInfo 'sample/sample_txt4.txt' at 0x7fe14b53a368>]
```

Single file extraction

```python
import tarfile

file_name = "sample/sample_txt1.txt"
with tarfile.open("sample.tar", "r") as tf:
    print("Opened tarfile")
    tf.extract(member=file_name, path="./extraction_dir")
    print(f"{file_name} extracted")
```

## Writing a tar file

To add files to a tar file, user has to open the file in append mode and use `tarfile.TarFile.add` method, it takes the path of file to be added as a parameter.

```python
import tarfile

file_name = "sample_txt5.txt"
with tarfile.open(f"./sample.tar", "a") as tf:
    print("Opened tarfile")
    print(f"Members before addition of {file_name}")
    print(tf.getmembers())
    tf.add(f"{file_name}", arcname="sample")
    print(f"Members after addition of {file_name}")
    print(tf.getmembers())
```

