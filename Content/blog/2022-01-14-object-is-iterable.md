---
title: How to check if an object is iterable in Python
date: 2022-01-14 00:00
description: Three methods to check iteration status of a variable in python.
tags: Python, Basics
path: object-is-iterable
author: Pratik Choudhari
---

An iterable is an object which can be traversed. Data structures like array, string, and tuples are iterables.

In certain cases, e.g., when dealing with custom data types, we may not know whether an object is iterable, but for this there should be some kind of mechanism through which a user can estimate its iterable status.

In this article, we will see how we can identify if an object is iterable using three techniques.

## 1. Iterating over the object
This is the simplest way to check if an object is iterable.

```python
try:
  _ = [element for element in target_variable]
except TypeError:
  print("Object not an iterable")
else:
  print("Object is iterable")
```

This style of programming is called duck typing ("If it looks like a duck and quacks like a duck, it must be a duck.").

## 2. Using `iter()`
If an object is iterable, it will not throw an error when used with `iter()`. It checks if the passed object has `__iter__()` or `__getitem__()` method available, 
which are methods that iterables possess.

```python
try:
  iter(target_variable)
except TypeError:
  print("Object not an iterable")
else:
  print("Object is iterable")
```

## 3. Using collection.abc.Iterable
The [`collection`](https://docs.python.org/3/library/collections.html) library houses specialized container datatypes and abstract base classes to test if a 
class provides particular interfaces. Coupled with built-in `isinstance()` method we can get a boolean response. This technique does not work with classes that implement `__getitem__()` dunder method.

```python
from collection.abc import Iterable

if isintance(target_variable, Iterable):
  print("Object is iterable")
else:
  print("Object not an iterable")

```
