---
title: How to flatten a list of lists in Python
date: 2022-01-01 00:00
description: Know how vanilla Python and a few standard libraries can be used to flatten a list of lists.
tags: Python, Basics
path: flatten-list-of-lists
author: Pratik Choudhari
---

A flat list is a type of list which is not nested, for example:

```python
["h", "e", "l", "l", "o"]
[True, 1, 2, False]
```

And nested lists:

```python
[[7], [0, 9, 3], [4, 6, 8]]
[["lorem", "ipsum", "seth", "sir"], ["domat", "texeto", "do"]]
```

There are several ways in which a nested list can be unpacked and made into a flat list, some of these approaches don’t need a library whereas others use [itertools](https://docs.python.org/3/library/itertools.html), 
[functools](https://docs.python.org/3/library/functools.html) and [numpy](https://numpy.org/).

### 1. Looping
This is the easiest way to flatten a list. It uses a for loop to iterate over the main list and another nested for loop to iterate over the element of the main list.
```python
nested_list = [[1, 2, 3], [4, 5, 6], [7], [8, 9]]
flat_list = []
for sublist in nested_list:
  for element in sublist:
    flat_list.append(element)
print(flat_list)
```

Output:
```console
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

Alternatively, extend() can be used to create the resulting list without nested loops
```python
flat_list = []
for sublist in nested_list:
  flat_list.extend(element)
```

### 2. itertools.chain(*nested_list)
Itertools is part of python’s standard libraries and provides a method to create a flat list. 
The chain method takes lists as arguments, therefore a `*` is used to unpack the list, read more about *args [here](https://www.python-engineer.com/blog/args-kwargs/), the return value is an iterator and not a list, using list() it is forced to yield all elements.
```python
import itertools

nested_list = [[1, 2, 3], [4, 5, 6], [7], [8, 9]]
flat_list = itertools.chain(*nested_list)
flat_list  = list(flat_list)
```

### 3. itertools.chain.from_iterable(nested_list)
Similar to itertools.chain() but takes a nested list as argument.

```python
import itertools

nested_list = [[1, 2, 3], [4, 5, 6], [7], [8, 9]]
flat_list = itertools.chain.from_iterable(nested_list)
flat_list  = list(flat_list)
```

### 4. functools.reduce(function, nested_list)
reduce() works by applying a function to two elements of an iterable cumulatively.

```python
from functools import reduce

nested_list = [[1, 2, 3], [4, 5, 6], [7], [8, 9]]
flat_list = reduce(lambda x, y: x+y, nested_list)
```

Alternatively, instead of writing lambda function, in-built [operator.concat](https://docs.python.org/3/library/operator.html#operator.concat) can be used.

```python
import operator
from functools import reduce

nested_list = [[1, 2, 3], [4, 5, 6], [7], [8, 9]]
flat_list = reduce(operator.concat, nested_list)
```

### 5. numpy.concatenate(nested_list)
Returns merged list instead of an iterator 
```python
import numpy

nested_list = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
flat_list = numpy.concatenate(nested_list)
```

### 6. numpy.array(nested_list).flat
Numpy arrays have a flat property which can be used to get an iterator for a flattened array but it only works if lists inside a nested list are of same lengths.

```python
import numpy

nested_list = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
print(list(numpy.array(nested_list).flat))
```

Output:
```console
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

If sub lists are not of same length
```python
import numpy

nested_list = [[1, 2, 3], [4, 5], [7, 8, 9]]
print(list(numpy.array(nested_list).flat))
```

Output:
```console
[[1, 2, 3], [4, 5], [7, 8, 9]]
```
