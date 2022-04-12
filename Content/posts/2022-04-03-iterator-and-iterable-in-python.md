---
title: Difference between iterator and iterable in Python
date: 2022-04-12 00:00
description: Learn the difference between iterator and iterable in Python.
tags: Python, Basics
path: iterable-vs-iterator
author: Shweta Goyal
---

Iteration is a process of using a loop to access all the elements of a sequence. Most of the time, we use *for loop* to iterate over a sequence. But there are some times when we need to iterate over a sequence using a different approach. In those cases, we need to use an **iterator**.

In Python, both the terms **iterators** and **iterables** are sometimes used interchangeably but they have different meanings.

**We can say that an iterable is an object which can be iterated upon, and an iterator is an object which keeps a state and produces the next value each time it is iterated upon.**

**Note:** Every iterator is an iterable, but not every iterable is an iterator.

Let's see the difference between iterators and iterables in Python.

## Iterable in Python

**Iterable is a sequence that can be iterated over**, i.e., you can use a *for loop* to iterate over the elements in the sequence:

```python
for value in ["a", "b", "c"]:
    print(value)
```

Examples are:

- Lists
- Tuples
- Strings
- Dictionaries
- Sets
- Generators

Iterable objects are also known as iterable containers.

**Note:** **We can create an iterator object from an iterable by using the `iter()` function** since the `iter()` function returns an iterator from an iterable object. More about this later. But when using iterables, it is usually not necessary to call `iter()` or deal with the iterator objects yourself. The *for* statement does that automatically, creating a temporary unnamed variable to hold the iterator for the duration of the loop ([Python docs](https://docs.python.org/3/glossary.html#term-iterable)).

Let’s see an example:

```python
colors = ['Black', 'Purple', 'Green']
for color in colors:
    print(color)
```

Output:

```console
Black
Purple
Green
```

## Iterator in Python

An iterator is an object which must implement the iterator protocol consisting of the two methods `__iter__()` and `__next__()` (see [Iterator Types](https://docs.python.org/3/library/stdtypes.html#iterator-types)).

An iterator contains a countable number of values and can return the next element in the sequence, one element at a time.

Implementing `__iter__()` is required to allow both containers and iterators to be used with the *for* and *in* statements.

Implementing `__next__()` specifies how to return the next item from the iterator. If there are no further items, a `StopIteration` exception should be raised.

After implementing `__iter()__` and `__next__()`, we can also explicitly call `iter()` and `next()`:

### 1) `iter()`

The `iter()` function returns an iterator object. It takes any collection object as an argument and returns an iterator object. We can use the `iter()` function to convert an iterable into an iterator.

Let’s see how to use the `iter()` function:

```python
iterator = iter(object)
```

Example:

```python
colors = ['Black', 'Purple', 'Green']
iterator = iter(colors)
print(iterator)
```

Output:

```console
<list_iterator object at 0x7f8b8b8b9c18>
```

An iterator can also be converted back to a concrete type:

```python
colors = list(iterator)
print(colors)
```

Output:

```console
['Black', 'Purple', 'Green']
```

### 2) `next()`

The `next()` function is used to get the next item from the iterator. If there are no further items, it raises a `StopIteration` exception. The `__next__()` method is called automatically when the *for* statement tries to get the next item from the iterator.

Let’s see how to use the `next()` function:

```python
colors = ['Black', 'Purple', 'Green']
iterator = iter(colors)
print(next(iterator))  # Output: Black
print(next(iterator))  # Output: Purple
print(next(iterator))  # Output: Green
print(next(iterator))                    

# Output:
# Traceback (most recent call last):
#   File "iterator-and-iterable-in-python.py", line 31, in <module>
#     print(next(iterator))
# StopIteration
```

## Why not every iterable is an iterator

Earlier we said every iterator is an iterable, but not every iterable is an iterator. This is for example because we cannot use `next()` with every iterable, so it does not follow the iterator protocol:

```python
a = [1, 2, 3]
next(a)

# Traceback (most recent call last):
#  File "<stdin>", line 1, in <module>
# TypeError: 'list' object is not an iterator
```

On the other hand, for every iterator we can call `next()`, and we can also loop over it with a *for* and *in* statement.

## Conclusion

In this tutorial, we have learned about iterators and iterables in Python. We have also learned how to use `iter()` and `next()` functions. To learn more about iterators, check out the Python documentation on [iterators](https://docs.python.org/3/howto/functional.html#iterators).
