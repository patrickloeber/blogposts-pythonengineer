---
title: What are *args and **kwargs in Python
date: 2021-12-24 00:00
description: Understand the purpose and usage of args and kwargs in python functions with examples.
tags: Python, Basics
path: args-kwargs
author: Pratik Choudhari
---

The concept of args and kwargs is one of the most important things to understand in python. It is frequently asked in technical interview rounds. 
To understand \*args and \*\*kwargs you will need to know about sequence and dictionary unpacking in python, we already have a blog explaining these parts, check it out [here](https://www.python-engineer.com/courses/advancedpython/19-asterisk/). 


## Why are args and kwargs required?

Sometimes, we don’t know how many non-keyword arguments a function can receive thus there was a need for a mechanism that can allow a function to receive any number of arguments and the solution was \*args, args being a sequence data structure. 
It is important to focus on the non-keyword aspect of this. 

On the other hand, we also might need to know the name of multiple arguments passed. 
In this case, we use \*\*kwargs, kwargs being a dictionary with key as argument name and value as the argument value.

## How to use \*args and \*\*kwargs?

## Working with *args

Let’s understand this with an example, suppose we have to write a function to add numbers. 
A simple way to go with this is to have a single argument as a list of numbers. 

```python
def add(numbers: list):
    return sum(numbers)

print(add([10, 20, 30 , 40, 50]))
```

Output:

```console
150
```

Now, let’s say we don’t have to pass a list and instead directly pass the numbers to add as arguments.

```python
def add(*args):
    return sum(args)

print(add(756, 9, 54, 59, 90))
```

Output:

```console
968
```

The arguments passed to add() are converted into a tuple of numbers when entering into the function logic, this way we have a single function parameter that is iterable. 
The order of elements in args does not matter.

### Working with \*\*kwargs

When using kwargs we have to use a dictionary. 
A function is_square() takes two keyword arguments, number and square_value, it returns True if number squared is equal to square_value else False.

```python
def is_square(number: int, square_value: int):
    if number ** 2 == square_value:
        return True
    return False
```

Normally, this function will be called as

```python
print(is_square(number=12, sqaure_value=144))
```

Output:

```console
True
```

While using kwargs we do it like

```python
parameters = {“number”: 12, “sqaure_value”: 169}
print(is_square(**parameters))
```

Output:

```console
False
```

Here, the dictionary values will be unpacked and passed as keyword arguments to the function.

### Working with \*args and \*\*kwargs combined

Yes, args and kwargs can be combined together in a function. 
To demonstrate this, let’s create a function that will calculate the mean, median, or mode of distribution, it takes a list of numbers(a distribution) and a keyword argument indicating the type of measure.

```python

import numpy as np
from scipy import stats

def central_tendency(*args, **kwargs):
    if kwargs[“measure”] == “mean”:
        return np.mean(args)
    elif kwargs[“measure”] == “median”:
        return np.median(args)
    elif kwargs[“measure”] == “mode”:
        return stats.mode(args).mode
    else:
        print(“Invalid operation”)

kwarg = {“measure”: “mean”}
print(central_tendency(15, 55, 63, 88, 155, **kwarg))
```

Output:

```console
75.2
```
