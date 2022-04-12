---
title: Type Conversion in Python
date: 2022-04-13 00:00
description: Learn the different ways to convert a data type to a different data type in Python.
tags: Python, Basics
path: type-conversion
author: Shweta Goyal
---

There are times when you want to convert a [data type](https://docs.python.org/3/library/datatypes.html) to a different data type. This is called **type conversion**.

There are two types of type conversion in Python: **Implicit** and **Explicit**. Let's learn more about them with some examples.

## Implicit Type Conversion

In implicit Type Conversion, the Python interpreter converts one data type to another data type automatically during run time. To avoid data loss, Python converts the lower data type to a higher data type.

Let’s see an example to understand more:

```python
number1 = 10    # integer
number2 = 20.5  # float
sum_addition = number1 + number2

print(sum_addition)        # Output: 30.5
print(type(sum_addition))  # Output: <class 'float'>
```

In the above example, the addition of two variables, i.e., an integer (smaller) data type and a float (higher) data type gives you a float data type as a result. Python automatically transforms the data type to a float data type without losing any information.

However, implicit conversion does not work in all cases. Let’s see what happens when you try to add an integer and a string:

```python
value1 = 10    # integer
value2 = "10"  # string
sum_addition = value1 + value2

## Output:
Traceback (most recent call last):
  File "<pyshell#6>", line 1, in <module>
    sum = value1 + value2
TypeError: unsupported operand type(s) for +: 'int' and 'str'
```

In the above example, the addition of two variables, i.e., an integer (smaller) data type and a string (higher) data type gives you a *TypeError*. Python doesn’t convert the string to an integer data type. That’s where you need to convert the values explicitly.

## Explicit Type Conversion

In explicit Type Conversion, you need to convert the values explicitly with the help of predefined functions like `int()`, `float()`, `str()`, `bool()`, etc.

This is also known as **typecasting**. In this process, there are chances of data loss as you are converting the value to a lower data type.

Let’s see an example to understand more:

```python
value1 = 10          # integer
value2 = "10"        # string

# Type casting value2 of string to integer
value2 = int(value2)
sum_addition = value1 + value2
print(sum_addition)        # Output: 20
print(type(sum_addition))  # Output: <class 'int'>
```

In the above example, we have explicitly converted the string to an integer data type using an `int()` function. Now, the addition works and also gives you an integer data type as a result.

Let's see an example of explicit typecasting from a higher datatype (float) to a lower datatype (integer):

```python
value = 10 .5       # float
value = int(value)  # int

print(value)  # 10
```

The example above demonstates that now we lost data information, i.e., the floating point precision.

There are so many built-in functions in Python to convert data types. You can see the list of all the built-in functions in Python in the [Python Data Types](https://docs.python.org/3/library/functions.html) section.

## Conclusion

In this tutorial, we have learned about the different ways to convert a data type to a different data type in Python. We have also learned about the implicit and explicit type conversion in Python. This is a very important topic to understand when you are working with Python.
