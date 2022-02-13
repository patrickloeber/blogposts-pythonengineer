---
title: What is the meaning of single and double leading underscore in Python
date: 2022-02-13 00:00
description: Know how number of underscores affect accessibility of variables with examples.
tags: Python, Basics
path: double-single-leading-underscore
author: Pratik Choudhari
---

Python does not have access identifiers like public, private and protected. Single and Double underscores are used as alternatives for pseudo access restriction. 

In this article, we will understand the usage of single and double underscores in variable names.

## 1. Single underscore

Variables declared in class with single leading underscore are to be treated as private by convention, it works as a weak indicator to signify internal use only. 

Outside a class, such variables do not have any special significance, they are treated as a public variable.

When importing objects from a file, if `from module import *` is used Python does not import objects whose name start with a single leading underscore.

Example:
```python
class Sample:
def __init__(self):
    self.foo = "lorem"
    self._bar = "ipsum"

S = Sample()
print(s.foo, s._bar)
```

Output:
```console
lorem ipsum
```

Through this example, we can see that there is no access restriction imposed by python on `_bar` however an IDE such as PyCharm would generate a warning about usage of this pseudo private variable outside class `Sample`.

## 2. Double underscore

Inside a class, when a variable name has two leading underscores it is renamed to `_classname__variable`, this process is called as **Name Mangling** and it helps Python distinguish between the same variable names from different classes.

Here too, if `from module import *` is used Python does not import objects whose names start with double leading underscore.

Example:

```python
class Sample:
    def __init__(self):
        self.foo = "hello"
        self.__bar = "world"

s = Sample()
print(dir(s))
```

Output:
```console
['_Sample__bar',...,'foo']
```

We can see that an instance of class `Sample` does not have a reference to `__bar`.

