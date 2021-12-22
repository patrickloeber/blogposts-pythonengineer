---
title: How to delete files and folders in Python
date: 2021-12-22 00:00
description: Delete files in python using os and shutil.
tags: Python, Basics
path: copy-files-python
author: Pratik Choudhari
---

In a previous blog, we discussed how to copy files using python. 
In this article, we will see how [*os*](https://docs.python.org/3/library/os.html) and [*shutil*](https://docs.python.org/3/library/shutil.html) libraries can be used to delete files and folders on a computer. 
Both libraries come under standard python packages, so there’s no installation required. 

Let’s dive straight in.

## Deletion of files:

### 1. `os.remove(file_path)`

This is the most straightforward way to delete a file from the system, `file_path` must be a path-like python object. 
The behaviour of deletion operation differs based on Operation System, on Windows a file can not be deleted until it is being used by another application. 
On the other hand, on linux the file object is deleted but data on disk is not erased until the application using it releases the lock.

Errors thrown:
- IsADirectoryError
- FileNotFoundError

Examples:

```python
import os
os.remove(“/home/user/Documents/notes.txt”)
```

### 2. `os.rmdir(directory_path)`

Working of this function is similar to [rmdir](https://www.computerhope.com/unix/urmdir.htm) in linux. 
`directory_path` should be a python path-like object. 
If the directory specified in the path is not empty an error will be raised, implying that only empty directories can be deleted. 
pathlib.Path.rmdir() is an alternative to os.rmdir() with the exact same behaviour.

Errors thrown:
- FileNotFoundError
- OSError

Examples:

```python
import os
os.rmdir(“/home/user/Desktop/Images”) 
```

### 3. `shutil.rmtree(directory_path)`

Shutil is associated with file operations and also includes a function that can be used to delete a directory and all of its contents recursively. 
It is similar to Linux [rm -rf](https://www.computerhope.com/unix/urm.htm) command. The directory path provided must not be a [symlink](https://www.computerhope.com/jargon/s/symblink.htm).

Errors thrown:
- FileNotFoundError
- NotADirectoryError

Examples:

```python
import shutil
shutil.rmdir(“/home/user/Desktop/Images”) 
```
