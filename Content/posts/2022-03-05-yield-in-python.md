---
title: What does the yield keyword do in Python
date: 2022-03-05 00:00
description: Understand the use of yield keyword with examples.
tags: Python, Basics
path: yield-in-python
author: Pratik Choudhari
---

The `yield` keyword in Python is used exclusively with [generators](https://www.python-engineer.com/courses/advancedpython/14-generators/) to return values on iteration. In this article, we will explore `yield` in terms of its use and purpose with examples.

# Purpose of `yield`

Generators are function like structures in Python, except on calling a generator we do not receive the output instead a generator object is returned. `return` keyword used in a normal function is analogous to `yield` in a generator. 

The generator returns an object only on iteration or when used with `next()`, when an object is yielded the state of the generator is saved in memory.

# Examples

Create a sequence from 0 to 9

**Using a function**

```python
def create_sequence():
    return [n for n in range(10)]

print(create_sequence())
```

Output:

```console
[1, 2, 3, 4, 5, 6, 7, 8, 9]
```

**Using generator**

```python
def create_sequence():
    for n in range(10):
        yield n
        
print("Calling the generator:", create_sequence())
print("Iterating over generator")

for n in create_sequence():
    print(n)
```

Output:

```console
Calling the generator: <generator object create_sequence at 0x7fd2806d80f8>
Iterating over generator
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


