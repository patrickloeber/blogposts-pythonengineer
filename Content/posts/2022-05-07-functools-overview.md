---
title: What is functools in Python?
date: 2022-05-09 00:00
description: Introduction to the higher-order functions library of Python
tags: Python, Basics
path: functools-overview
author: Pratik Choudhari
---

[Functools](https://docs.python.org/3/library/functools.html) is one of the most useful Python standard libraries which contains a collection of higher-order functions.

The member functions have a variety of utilities, including **caching**, **cumulative operations**, and **partial functions**. 

In this article, we will understand what exactly higher-order functions are and get an overview of a few handy functions in this module.

## Higher-order functions

A function is defined as a piece of code that takes arguments, which act as input, does some processing involving these inputs and returns a value (output) based on the processing.

When either a function takes another function as an input or returns another function as output then such functions are called higher-order functions. `map()`, `reduce()` and `filter()` are all higher-order functions.

Example of a custom higher-order function:

```python
def create_function(aggregation: str):
    if aggregation == "sum":
        return sum
    elif aggregation == "mean":
        def mean(arr: list):
            return sum(mean)/len(mean)
        return mean
    return None
```

## The functools module

As mentioned earlier, *functools* gives us access to functions which either take or return another function. The most commonly used functions from this module are:

- 1. reduce
- 2. partial
- 3. cache
- 4. lru_cache
- 5. wraps

We will understand every function with examples

## functools.reduce()

This function takes two arguments, a function and an iterable. The input function is applied on the next iterable element with the result from the last run, which results in an output which is cumulative.

The following example shows how to calculate the sum of a list using reduce.

```python
from functools import reduce
print(reduce(lambda x, y: x + y, [1, 2, 3]))
# 6
```

## functools.partial()

`partial()` returns an object which behaves like a partially initialized target function with given arguments and keyword arguments.

```python
from functools import partial

def target_func(arg_one, arg_two):
    print(f"arg_one = {arg_one}, arg_two = {arg_two}")

partial_one = partial(target_func, arg_two="World!")
partial_two = partial(target_func, arg_one="Love")

partial_one(arg_one="Hello")
partial_two(arg_two="Python")
```

Output:
```console
arg_one = Hello, arg_two = World!
arg_one = Love, arg_two = Python
```

Explanation:

The first argument of `partial()` is a function which we need to partially initialize. All arguments passed after the first one are passed on to the target function.

The object returned can be called like a normal function with the remaining arguments. 

## @functools.cache

`cache` is used as a decorator and is able to cache the return values of a function based on inputs. It is available in Python 3.9 and above. 

The cache size is unbounded and therefore the cached dictionary can grow to enormous sizes. 

Example:

```python
from functools import cache

@cache
def fibonacci(n):
    if n in [0, 1]:
        return n
    else:
        return fibonacci(n-1) + fibonacci(n-2)

print(fibonacci(4)) # called 5 times
print(fibonacci(11)) # called 7 times rather than 12 times
```

Output:
```console
3
89
```

## @functools.lru\_cache(maxsize=None)

A better alternative to the `@cache` is `@lru_cache` because the latter can be bounded to a specific size using the keyword argument maxsize.

Since the cache size can be limited there needs to be a mechanism that decides when to invalidate a cache entry. The mechanism used here is LRU (Least Recently Used). 

`@lru_cache(maxsize=10)` means only 10 most least recently used entries will be kept in the cache. As new entries arrive the oldest cache entries get discarded.

```python
from functools import lru_cache

@lru_cache(maxsize=2)
def fibonacci(n):
    if n in [0, 1]:
        return n
    else:
        return fibonacci(n-1) + fibonacci(n-2)

print(fibonacci(4))
# called 8 times rather than 5 times when @cache was used
print(fibonacci(11))
# called 81 times rather than 7 times when @cache was used
```

## @functools.wraps

To understand what `wraps` does one needs to understand what are decorators and how they work in Python. 

A decorator is essentially a function which takes another function as input, does some processing and returns the function.

When a decorator is used on a function, the function loses information about itself.

To understand this issue better lets look an example

```python
from time import time

def timeit(func):
    def inner_timeit(*args, **kwargs):
        """
        function to find execution time of another function
        """
        start = time()
        func(*args, **kwargs)
        print(f"Function ran in {time() - start} seconds")
    return inner_timeit

@timeit
def print_range(n: int):
    """
    prints numbers from 1 to n
    """
    for i in range(1, n+1):
        print(i)

print(print_range.__name__)
print(print_range.__doc__)
```

Output:

```console
inner_timeit
    function to find execution time of another function
```

`print_range` was decorated by `timeit` and it was essentially replaced by `inner_timeit`. Using `@wraps(func)`, this problem can be solved.

Solution:

```python 
from time import time
from functools import wraps

def timeit(func):
    @wraps(func)
    def inner_timeit(*args, **kwargs):
        """
        function to find execution time of another function
        """
        start = time()
        func(*args, **kwargs)
        print(f"Function ran in {time() - start} seconds")
    return inner_timeit

@timeit
def print_range(n: int):
    """
    prints numbers from 1 to n
    """
    for i in range(1, n+1):
        print(i)

print(print_range.__name__)
print(print_range.__doc__)
```

Output:

```console
print_range
    prints numbers from 1 to n
```

## Conclusion

In this article we've learned about the `functools` module in Python and its different functions.
