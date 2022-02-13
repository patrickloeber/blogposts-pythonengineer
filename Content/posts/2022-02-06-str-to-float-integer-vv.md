---
title: How to convert a string to float/integer and vice versa in Python
date: 2022-02-09 00:00
description: Learn type conversion between string, float, and integer in Python.
tags: Python, Basics
path: string-to-float
author: Pratik Choudhari
---

A data type defines the type of operations that can be performed on the data stored in a variable, these data types support type conversion which means to convert one data type into another based on some assumptions and rules.

In this article, we will see how a string data type can be converted into float/int and vice versa.

## 1. String to Float/Integer

Python has built-in functions that help a user in typecasting one format into another. Conversion from string to float is done using the `float()` function.

**Example:**

```python
number_as_string = "3.14159"
number_as_float = float(number_as_string)
print(number_as_float)
```

Output:
```console
3.14159
```

Typecasting an integer data type into a string is similar if the number to be converted is not a decimal number.

**Example:**

```python
number_as_string = "67"
number_as_integer = int(number_as_string)
print(number_as_integer )
```

Output:
```console
67
```

If the string value is a decimal number, using `int()` will through a `ValueError`.

First, the string value needs to be typecasted into a float and then into an integer. The result will include the whole number part of the float, as the decimal part is discarded during float to int conversion.

**Example:**

 ```python
number_as_string = "3.14159"
number_as_float = float(number_as_string)
number_as_integer = int(number_as_float)
print(number_as_integer)
```

Output:
```console
3
```

A `ValueError` is also thrown in any other case where the string cannot be converted to a number.
To be on the safe side, we could wrap the casting in a `try-except` block:

**Example:**

```python
try:
    number_as_string = "3.14aaa159"
    n = float(number_as_string)
except ValueError:
    print(f"{number_as_string} cannot be converted to a number")
```

## 2. Float/Integer to String

Both float and integer can be converted into a string using the `str()` function.

**Example:**

 ```python
number_as_float = 3.14159
number_as_string = str(number_as_float)
print(number_as_string, type(number_as_string))

number_as_integer = 67
number_as_string = str(number_as_integer)
print(number_as_string, type(number_as_string))
```

Output:
```console
3.14159 <class 'str'>
67 <class 'str'>
```
