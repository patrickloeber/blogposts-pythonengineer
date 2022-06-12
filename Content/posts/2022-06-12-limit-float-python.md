---
title: How to limit float values to N decimal places in Python
date: 2022-06-12 00:00
description: A handy trick using format specifiers.
tags: Python, Basics
path: limit-float-python
author: Pratik Choudhari
---

A float data type is a numeric data type with decimal places. In some cases, float values can go to hundreds of decimal places; therefore, we need to truncate the value to view only the first N decimal places.

This article will show how we can limit a float number to N decimal places using a format specifier.

## What are format specifiers?

Format specifiers define how data is to be printed on standard output, it includes doing operations like truncating values and extending values.

All major programming languages have this feature.

## Limiting decimal places in Python

The format specifier we need here is `.Nf` where `N` is the number of decimal places expected in output. It is important to note that this does not round values to the Nth decimal place. There are two ways to implement this, the first is using f-strings and the second is using the format property of strings.

Using f-strings

```python
number = 3.142857142857143
print("Limited float value:", f"{number:.2f}")
```

Output:

```console
Limited float value: 3.14
```

Using format property

```python
number = 3.142857142857143
print("Limited float value: {:.2f}".format(number))
```

Output:

```console
Limited float value: 3.14
```

