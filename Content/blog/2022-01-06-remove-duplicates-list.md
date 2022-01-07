---
title: How to remove duplicate elements from a list in Python
date: 20221-01-06 00:00
description: Three ways in which lists in Python can be deduplicated.
tags: Python, Basics
path: remove-duplicates-list
author: Pratik Choudhari
---

A list data structure is capable of storing elements of different data types and multiple occurrences. 
In some cases, lists need to be deduplicated, which means we have to remove copies of elements from the data structure.
In this article, we will see how duplicates can be removed from a list using plain python and [numpy](https://numpy.org/)

### 1. Using Set
Set is made of only unique elements, duplicate insertions are ignored. In this approach, 
first the list is typecasted to a set and then typecasted back into a list.
```python
duplicate_list = [56, 4, 81, 56, 9, 4]
cleaned_list = list(set(duplicate_list))
print(cleaned_list)
```
Output
```console
[56, 81, 4, 9]
```
It is important to note that typecasting into a set does not preserve the order.

### 2. Using dict.fromkeys()
Using this approach, order can be preserved. `dict` in python has a method `fromkeys()` which takes in an iterable of hashable 
objects and creates a dictionary from them, while setting all values as None.
```python
duplicate_list = [56, 4, 81, 56, 9, 4]
cleaned_list = list(dict.fromkeys(duplicate_list))
print(cleaned_list)
```
Output
```console
[56, 4, 81, 9]
```

### 3. Using numpy.unique(duplicate_list)
Numpy is known for it’s versatility in dealing with array operations. Using [`numpy.unique()`](https://numpy.org/doc/stable/reference/generated/numpy.unique.html) does not preserve order rather it sorts the array in ascending order.
```python
import numpy as np
duplicate_list = [56, 4, 81, 56, 9, 4]
cleaned_list = list(np.unique(dupllicate_list))
print(cleaned_list)
```
Output
```console
[4, 9, 56, 81]
```
