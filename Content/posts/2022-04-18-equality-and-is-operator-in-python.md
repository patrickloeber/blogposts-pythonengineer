---
title: Difference between the equality operator and is operator in Python
date: 2022-04-29 00:00
description: Learn the difference between the equality operator and is operator in Python.
tags: Python, Basics
path: equality-vs-is-operator
author: Shweta Goyal
---

There are two operators in Python that are used to compare values: `==` and `is`. The `==` operator compares the values and `is` operator compares the references. Let’s see the difference between them:

## Equality (==) Operator

The equality operator is used to compare two values of the objects/variables. It returns `True` if both the values are equal and `False` if they are not equal. This is useful when you want to check if two objects contain the same content or not.

Let's see an example:

```python
value1 = 50
value2 = 50
value1 == value2    # Output: True

number1 = 50
number2 = 60
number1 == number2  # Output: False
```

The first check returns True as both the values are equal, and the second check returns False as the values are different.

## Identity (is) Operator

The identity operator is used to check if two variables are pointing to the same object in memory or not. This is useful when you want to check if the object is singleton like `None`, `True`, `False`, etc as they check for identity (Here, singleton means objects with one reference in memory). It also checks if the object is of a particular type or not.

Let's see an example:

```python
value1 = 50
value2 = 50
value1 is value2    # Output: True

## Checking the identities (location) of objects
id(value1)       # Output: 2777565955856
id(value2)       # Output: 2777565955856
```

In the above example, the result of the identity operator is True as both the values have the same location in the memory. `id()` is the Python built-in function that returns the memory location of an object.

Let's see another example:

```python
number1 = 500
number2 = 500
number1 is number2    # Output: False

## Checking the identities (location) of objects
id(number1)       # Output: 2777601717424
id(number2)       # Output: 2777601717488
```

In the above example, the result of the identity operator is False as both the values have different locations in the memory.

You can see that when we have small numbers like 50 in the first example, they have same the memory locations. But when we have large numbers like 500 in the second example, they have different memory locations. Why?

This is because interpreters in CPython [interns](https://docs.python.org/3.7/library/sys.html?highlight=sys.intern#sys.intern) smaller numbers to a fixed memory location to save memory as they are frequently used. Generally, the range of numbers is -5 to +256 but it can vary according to your interpreter. Any number outside of this range is interned to a different memory location. That's why large number like 500 returns False.

## Conclusion

In this tutorial, you have learned the difference between the `equality` operator and the `is` operator. You have also learned how to use them. The difference between the `equality` operator and `is` operator is that `is` operator checks the identity of the objects and `equality` operator checks the equality of the objects.

