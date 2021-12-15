---
title: How to copy files in Python
date: 2021-12-15 00:00
description: Learn how to leverage the shutil package to copy files in python.
tags: Python, Basics
path: copy-files-python
author: Pratik Choudhari
---

Python is widely used as an automation tool and one of the major automation tasks is copying files from a source to a destination. 

Many would find the os library synonymous with such tasks but it’s surprising that os doesn’t provide support for copying or moving files. 

In this article, we are going to see how we can use the shutil module to help us move files from one path to another.

### About `shutil`

Shutil is amongst built-in modules of python. It provides access to some high-level operations such as changing ownership of files, using which command and operations pertaining to files such as copying, moving, archiving, and removal. 

There are four ways to copy files in shutil:

### 1. shutil.copy(src, dest)

This function takes in two arguments, the source file path and destination path, both must be a string or bytes object. Source must be file name with path and destination can be file path or directory. If the file name in source and destination is different then the source file will be copied to a new file with specified name. Using copy() preserves file permissions but losses it’s metadata.
Here's an example:

```python
import shutil

shutil.copy("/home/user/Desktop/notes.txt", "/home/user/Documents/class_notes.txt") # file will be renamed to class_notes
shutil.copy("/home/user/Desktop/notes.txt", "/home/user/Documents/") # file will be copied with same name
```

### 2. shutil.copyfile(src, dest)

Copyfile() is same as copy() with a few differences. Destination path can not be a directory, it must be a path to new file. Metadata and permissions are not preserved.

### 3. shutil.copyfileobj(src_obj, dest_obj)

In cases where file objects are required to copy files, copyfileobj() can be used. Here, source and destination are both file objects. Metadata and permissions are not preserved.
Let's see the usage:

```python
import shutil

src_obj = open("/home/user/Desktop/notes.txt", "r")
dest_obj = open("/home/user/Documents/notes.txt", "w") # file name can be different

shutil.copyfileobj(src_obj, dest_obj)

src_obj.close()
dest_obj.close()
```

### 4. shutil.copy2(src, dest)

copy2() is identical to copy(), except that copy2() preserves metadata.

