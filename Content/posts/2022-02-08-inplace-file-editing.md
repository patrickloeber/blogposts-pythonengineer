---
title: In-place file editing with fileinput module
date: 2022-02-10 00:00
description: This post shows how to edit one or more files in-place using the fileinput module.
tags: Python, Basics
path: inplace-file-editing
author: Sundeep Agarwal
---

Often, I have to make changes to existing files. For example, some software got updated, so I've to change version numbers. Or perhaps, I've changed the name of assets like input files, images, etc. If it's a single file, I'd likely just use my favorite text editor to open the file, make the changes and save it. If I have to edit multiple files, I'll write a Python script instead.

In this post, you'll learn how to use the `fileinput` module to make changes and update the original files.

### Documentation

It is always a good idea to know where to find the documentation. Here's a quote from [docs.python: fileinput](https://docs.python.org/3/library/fileinput.html):

> This module implements a helper class and functions to quickly write a loop over standard input or a list of files. If you just want to read or write one file see `open()`.

And here's the specific method you'll be learning to use in this post:

```python
fileinput.input(files=None, inplace=False, backup='', *, mode='r',
                openhook=None, encoding=None, errors=None)
```

### Passing files as CLI arguments

Assume you have two text files as shown below:

```console
$ ls *.txt
notes.txt  tools.txt

$ cat tools.txt
/home/learnbyexample/programs/command_help.sh
/home/learnbyexample/bkp/calc.py
/home/learnbyexample/programs/remove_duplicates.sh
/home/learnbyexample/programs/calc.py

$ cat notes.txt
Tool: /home/learnbyexample/programs/remove_duplicates.sh
    * retains only first copy of duplicate lines
    * maintains input order
```

Suppose you changed your folder name from `programs` to `bin`, here's one way to update the above two text files using the `fileinput` module. By default, the `inplace` argument is `False`, so you have to set it to `True` when you want to write back the changes to the original files. The `print()` function is used to display the output text which will then be redirected to the original files by the `fileinput` module.

```python
# change_path.py
import fileinput

with fileinput.input(inplace=True) as f:
    for ip_line in f:
        op_line = ip_line.replace('/programs/', '/bin/')
        print(op_line, end='')
```

Note that the input filenames aren't specified in the above program. Instead, you'll pass them as command line arguments as shown below:

```console
$ python3 change_path.py *.txt

$ cat tools.txt
/home/learnbyexample/bin/command_help.sh
/home/learnbyexample/bkp/calc.py
/home/learnbyexample/bin/remove_duplicates.sh
/home/learnbyexample/bin/calc.py

$ cat notes.txt
Tool: /home/learnbyexample/bin/remove_duplicates.sh
    * retains only first copy of duplicate lines
    * maintains input order
```

### stdin data

If there's no file to process, `fileinput.input()` will automatically use `stdin` data. If `inplace` is set to `True`, it'll be ignored.

Here's an example to show how the program discussed in the previous section will work with `stdin` data:

```console
$ echo '/home/user/programs/create_venv.py' | python3 change_path.py
/home/user/bin/create_venv.py
```

### Passing list of files

If you already know the files that have to be changed, you can pass them to the `files` argument. You can pass a single filename or an iterable of filenames.

```python
# file_list.py
import fileinput

ip_files = ('notes.txt', 'tools.txt')
with fileinput.input(files=ip_files, inplace=True) as f:
    for ip_line in f:
        op_line = ip_line.replace('/programs/', '/bin/')
        print(op_line, end='')
```

Now that you've already specified the files to be modified, you just have to execute the program without any additional CLI arguments:

```console
$ python3 file_list.py
```

Passing file arguments via CLI has the advantage of using shell features such as wildcard expansion. Python has various modules in case you need such features within the script itself. For example, you can use the [glob module](https://docs.python.org/3/library/glob.html) for wildcard expansion.

### Backups

Ideally, you should create backups of the files being modified so that you can recover original files if something goes wrong.

Assume you want to change `blue` to `brown` for the file shown below:

```console
$ cat colors.txt
red blue green
teal magenta
dark-blue sea-green
```

You can use the `backup` argument to create copies of the original files with the given extension.

```python
# inplace_with_backups.py
import fileinput

with fileinput.input(files='colors.txt', inplace=True, backup='.orig') as f:
    for ip_line in f:
        op_line = ip_line.replace('blue', 'brown')
        print(op_line, end='')
```

After you execute the above program, you'll see that there's a copy of the original file.

```console
$ python3 inplace_with_backups.py

# modified file
$ cat colors.txt
red brown green
teal magenta
dark-brown sea-green

# copy of the original file
$ cat colors.txt.orig
red blue green
teal magenta
dark-blue sea-green
```

Hope you found this post useful. Happy learning :)

