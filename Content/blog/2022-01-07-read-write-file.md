---
title: How to read and write files in Python
date: 2022-01-07 00:00
description: An easy guide to master file handling in Python.
tags: Python, Basics
path: read-write-file
author: Pratik Choudhari
---

Python has in-built functions which can be used to perform file operations such as opening a file, reading its content, writing content, and closing a file.

The term `file` can be defined as a container that is used to store data on computers, these containers can be referenced by a name called *filename*.

In general, when working with files, the following process is followed:

1. Opening of a file
2. Read/Write content
3. Closing of file

## 1. Opening a file
[`open()`](https://docs.python.org/3/library/functions.html#open) function is used to open a file in Python, the return value of `open()` is a python file pointer or a handler that points to the file on the computer. Hence, any further operations on a file have to be performed via a python file object.

`open()` has one required argument, *file*, which is the path to the target file.

Python supports multiple modes to open a file, all are listed below:

- r : open for reading (default)
- w : open for writing, truncating the file first
- a : open for writing, appending to the end of the file if it exists
- x : open for exclusive creation, failing if the file already exists
- b : binary mode
- t : text mode (default)
- \+ : open for updating (reading and writing)


When *mode* is not specified, the default mode is "r"
 
Example:

## 1. Opening in reading mode
```python
file_pointer = open("/home/user/foo.txt")
print(file_pointer)
```

Output:
```console
<_io.TextIOWrapper name='foo.txt' mode='r' encoding='UTF-8'>
```

2. Opening in write mode
```python
file_pointer = open("/home/user/foo.txt", "w")
print(file_pointer)
```

Output:
```console
<_io.TextIOWrapper name='foo.txt' mode='w' encoding='UTF-8'>
```

## 2. Reading file contents
File handlers create using `open()` are used to read file contents using three methods, we will understand the working of each with examples.

### - fp.read()
`read()` is used to read the contents of a file, this method takes an optional `size` argument, which specifies the number of characters to read. If no size is specified entire file contents are read by default.

Example:

Reading entire contents
```python
file_pointer = open("/home/user/foo.txt")
contents = file_pointer.read()
print(contents)
```

Output:
```console
'Primary colors:\n1. Red\n2. Green\n3. Blue\n'
```

Note: After reading all file contents and re-executing `fp.read()` an empty string will be returned, this is because `fp.read()` maintains a cursor on file content and does not reset by default. The `fp.seek(position)` method is used to seek the cursor.
  
Reading first 5 characters
```python
file_pointer = open("/home/user/foo.txt")
contents = file_pointer.read(5)
print(contents)
```

Output:
```console
'Prima'
```

Reading first 5 characters then next 7 characters
```python
file_pointer = open("/home/user/foo.txt")
contents = file_pointer.read(5)
print(contents)

contents = file_pointer.read(7)
print(contents)
```

Output:
```console
'Prima'
'ry colo'
```

### - fp.readline()
Reads a file line by line, returns a line as string. `fp.readline()` too maintains a cursor and therefore on re-execution yields next line.
a
Example:

```python
file_pointer = open("/home/user/foo.txt")
contents = file_pointer.readline()
print(contents)
```

Output:
```console
'Primary colors:\n'
```

### - fp.readlines()
`fp.readlines()` returns a list of lines from a file. Instead of using loops for getting all lines through `fp.readline()`, this function will provide user with a collection of all lines.

Example:

```python
file_pointer = open("/home/user/foo.txt")
contents = file_pointer.readlines()
print(contents)
```

Output:
```console
['Primary colors:\n', '1. Red\n', '2. Green\n', '3. Blue\n']
```

## 3. Writing contents to file

While writing files they must be opened in either of w(write), a(append), or x(exclusive creation) modes. Append mode allows only appending data to the file, write mode erases the file contents and overwrites the file and exclusive creation works similar to writing but the file being opened should not exist on the computer.

Example:

foo.txt before write:
```console
Primary colors:
1. Red
2. Green
3. Blue
```

Code:
```python
file_pointer = open("/home/user/foo.txt", "a")
file_pointer.write("\n")
file_pointer.write("Secondary colors:")
file_pointer.close()
```

foo.txt after write:
```console
Primary colors:
1. Red
2. Green
3. Blue

Secondary colors:
```
 
## 4. Closing file handles
Whenever a file pointer is opened, it is advised to close it after it is used, this is to make sure there are no dangling pointers in memory. 

Example:

```python
file_pointer = open("/home/user/foo.txt")
contents = file_pointer.readlines()
file_pointer.close()
print(contents)
```

Output:
```console
['Primary colors:\n', '1. Red\n', '2. Green\n', '3. Blue\n']
```


## File handling using a context manager

This is the preferred method for dealing with files. Context managers are used to making sure a resource is closed once it is used. The `with` statement in python is an in-built context manager, it spawns the resource once execution enters into the runtime context and closes the resource while exiting.

Example:

```python
with open("/home/user/foo.txt") as file_pointer:
  contents = file_pointer.readlines()
  print(contents)
```

Output:
```console
['Primary colors:\n', '1. Red\n', '2. Green\n', '3. Blue\n']
```

