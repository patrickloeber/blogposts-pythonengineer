---
title: How to count the occurrence of an element in a List in Python 
date: 2022-04-03 00:00
description: Learn four different ways in which the occurrence of an element in a List can be counted.
tags: Python, Basics
path: count-element-list
author: Pratik Choudhari
---

A common task when working with lists is to count the occurrence of an element.

There are a few ways through which we can achieve this, in this article we will go through these methods and understand them with examples.

## Using For loop

A simple for loop can be used with a counter variable which can be incremented every time the target element is found.

Example:

```python
target = 3
source_list = [1, 0, 3, 4, 3, 8, 3]

count = 0
for element in source_list:
    if element == target:
        count += 1
print("Element {target} occured {count} times in {source_list}")
```

Output:

```console
Element 3 occurred 3 times in [1, 0, 3, 4, 3, 8, 3]
```

## Using `count()` method

The `list` data structure in Python has a `count()` method which returns the count of an element given as a parameter.

Example:

```python
source_list = [1, 0, 3, 4, 3, 8, 3]

print(source_list.count(3))
```

Output:

```console
3
```

It is important to note that the `count()` method makes a complete pass over the list every time it is ran, therefore for counting multiple elements use the `collections.Counter` approach.

## Using `collections.Counter`

The Python standard library `collections` can be used to get a count of each and every element in a list. The value returned by the `Counter` method is a dictionary with the element and its count as key-value pairs.

Example:

```python
from collections import Counter

source_list = [1, 0, 3, 4, 3, 8, 3]

counts_dictionary = Counter(source_list)
print(counts_dictionary)
```

Output:

```console
Counter({3: 3, 1: 1, 0: 1, 4: 1, 8: 1})
```

## Using `operator.countOf()`

`operator` is amongst the standard libraries that come preinstalled with Python. Its `countOf()` method can be used to count the occurrence of an element in a list.

Example:

```python
from operator import countOf

source_list = [1, 0, 3, 4, 3, 8, 3]

print(countOf(source_list, 3))
```

Output:

```console
3
```
