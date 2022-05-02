---
title: Precision Handling in Python | floor, ceil, round, trunc, format
date: 2022-05-03 00:00
description: Learn the different methods for precision handling of floating-point numbers.
tags: Python, Basics
path: precision-handling
author: Shweta Goyal
---

Precision handling is a process of rounding off the values of floating-point numbers. Python has many built-in functions to handle the precision, like `floor`, `ceil`, `round`, `trunc`, and `format`. Let's discuss the different types of precision handling in Python.

Some of these methods require the `math` module to be imported.

## floor() function in Python

The `floor` function returns the largest integer less than or equal to a given number. Let's take an example to understand the floor function:

```python
import math

value = 34.185609
print(math.floor(value))
# 34

value = -34.185609
print(math.floor(value))
# -35
```

## ceil() function in Python

The `ceil` function returns the smallest integer greater than or equal to a given number. Let's take an example to understand the ceil function:

```python
import math

value = 34.185609
print(math.ceil(value)
# 35

value = -34.185609
print(math.ceil(value)
# -34
```

## trunc() function in Python

The `trunc` function returns the integer part of a number by removing all the decimal parts from a floating-point number. Let's take an example to understand the trunc function:

```python
import math

value = 34.185609
print(math.trunc(value))
# 34

value = -34.185609
print(math.trunc(value))
# -34
```

## round() function in Python

The `round` function rounds off the output in a customized format. We can pass the number of decimal places as an argument, and it then rounds a number to the given precision in decimal digits. Let's take an example to understand the round function:

```python
value = 34.185609

print(round(value, 2))
# 34.19
print(round(value, 3))
# 34.186
print(round(value, 4))
# 34.1856
```

**Interesting fact:** `round()` can also take a negative integer as second argument:

```python
value = 1346.185609

print(round(value, 0))
# 1346.0
print(round(value, -1))
# 1350.0
print(round(value, -2))
# 1300.0
print(round(value, -3))
# 1000.0
```

## Formatting with f-Strings in Python

f-Strings can be used to format values in a String:

```python
value = 34.185609

print(f'The value is: {value:.2f}')
# The value is: 34.19
print(f'The value is: {value:.3f}')
# The value is: 34.186
```

## format() function in Python

The `format` function can also be used to format the output. Let's take an example to understand the format function:

```python
value = 34.185609

print('The value is {0:.2f}'.format(value))
# The value is 34.19
```

## `%` formatting operator in Python

And similar, the `%` operator can be used to format and set the precision of the output:

```python
value = 34.185609

print('The value is: %.3f' % value)
# The value is: 34.186
```

## Conclusion

In this article, we have discussed the different types of precision handling in Python. We have also discussed the different types of formatting in Python.
