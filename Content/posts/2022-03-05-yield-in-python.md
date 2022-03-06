---
title: What does the yield keyword do in Python
date: 2022-03-08 00:00
description: Understand the use of yield keyword with examples.
tags: Python, Basics
path: yield-in-python
author: Pratik Choudhari
---

The `yield` keyword in Python is used exclusively with [generators](https://www.python-engineer.com/courses/advancedpython/14-generators/) to return values on iteration. In this article, we will explore `yield` in terms of its use and purpose with examples.

## Purpose of `yield`

Generators are function like structures in Python, except on calling a generator we do not receive the output, but instead a generator object is returned. The `return` keyword used in a normal function is analogous to `yield` in a generator.

The generator returns an object only on iteration or when used with `next()`. When an object is yielded the state of the generator is saved in memory.

## Examples of `yield`

Create a sequence from 0 to 9

### Using a function

```python
def create_sequence_func():
    return [n for n in range(10)]

print(create_sequence_func())
```

Output:

```console
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### Using a generator

```python
def create_sequence_gen():
    for n in range(10):
        yield n
        
print(create_sequence_gen())
```

Printing this will print only the generator object:

```console
<generator object create_sequence_gen at 0x7fd2806d80f8>
```

But when iterating over a generator we can access items like with a normal sequence:

```python
for n in create_sequence_gen():
    print(n)
```

Output:

```console
0
1
2
3
4
5
6
7
8
9
```

We could also convert a generator back to a list:

```python
print(list(create_sequence_gen()))
```

Output:

```console
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

Or we can create a generator object and access items with `next()`:

```python
gen = create_sequence_gen()
print(next(gen))
print(next(gen))
```

Output:

```console
1
2
```