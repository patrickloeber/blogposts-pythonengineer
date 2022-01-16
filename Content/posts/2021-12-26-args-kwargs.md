---
title: What are *args and **kwargs in Python
date: 2021-12-26 00:00
description: Understand the purpose and usage of args and kwargs in Python functions.
tags: Python, Basics
path: args-kwargs
author: Patrick Loeber
---

The concept of args and kwargs is a common use case found in function arguments in Python.

They allow an arbitrary number of arguments and keyword arguments to functions.

## *args

Using `*args` allows to pass an arbitrary number of function arguments.

Inside the function `*args` will give you all function parameters as a **tuple**:

```python
def foo(*args):
    for a in args:
        print(a)        

foo(1)
# 1

foo("Patrick", 30, 1)
# Patrick
# 30
# 1
```

## **kwargs

Using `**kwargs` allows to pass an arbitrary number of **keyword arguments**.

Inside the function `**kwargs` will give you all function parameters as a **dictionary**:

```python
def foo(**kwargs):
    for key, value in kwargs.items():
        print(key, value)        

foo(name="Pat", age="30")
# name, Pat
# age, 30
```

## Mixing args and kwargs

Both idioms can be mixed with normal arguments to allow a set of fixed and some variable length arguments:

```python
def foo(name, *args, **kwargs):
    print(name)

    for a in args:
        print(a)

    for key, value in kwargs.items():
        print(key, value)      


foo("Patrick", 30, 1, role='Software Engineer', level=3)
# Patrick
# 30
# 1
# role Software Engineer
# level 3
```

## Unpacking

Another usage of the `*var` or `**var idiom is to unpack argument sequences when calling a function.

- Lists/tuples/sets/strings can be unpacked into function arguments with one * if the length matches the parameters.
- Dictionaries can be unpacked with two ** if the length and the keys match the parameters.

```python
def foo(a, b, c):
    print(a, b, c)

# length must match
my_list = [1, 2, 3]
foo(*my_list)

my_string = "ABC"
foo(*my_string)

# length and keys must match
my_dict = {'a': 4, 'b': 5, 'c': 6}
foo(**my_dict)
```
Output:
```console
1 2 3
A B C
4 5 6
```

A more detailed look at all use cases of the asterisk (*) and double asterisk can be found in this [article](/courses/advancedpython/19-asterisk/). 
