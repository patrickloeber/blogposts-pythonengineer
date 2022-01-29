---
title: What are metaclasses in Python
date: 2022-01-29 00:00
description: A beginners guide to metaclasses in Python.
tags: Python, Basics
path: metaclasses
author: Pratik Choudhari
---

Everything is an object in python, including classes. Hence, if classes are an object, they must be created by another class also called as Metaclass.

![class hierarchy](../images/metaclass.png)

Metaclass is an advanced python concept and is not used in day-to-day programming tasks. They allow a user to precisely define a class state, change its attributes and control method behaviour. 

In this article, we will understand how metaclasses can be created and used in Python.

### 1. Understanding the `type()` function

To fully understand Metclasses, one needs to thoroughly understand `type()`. 

In Python, `type()` is used to identify the data type of a variable, if we have the following code

```python
var = 12
print(type(var))
```

Console output would be:

```console
<class 'int'>
```

Indicating `var` is an instance of the class `int`.

In the case of a user-defined class, we get the following output.

```python
class Foo:
    def bar():
        pass

foo_obj = Foo()
print("Type of Foo's instance is:", type(foo_obj))
print("Type of Foo is:", type(Foo))
```

```console
Type of Foo's instance is: <class '__main__.Foo'>
Type of Foo is: <class 'type'>
```

Here, we can see `foo_obj` is correctly identified as an instance of class `Foo` but the type of class `Foo` indicates that it is an instance of class `type`, establishing the point that classes are indeed created by other classes.

#### Creating classes dynamically using `type()`

This usage of `type()` is fairly unknown. The `type()` function takes three arguments.

```python
type(name: str, bases: tuple, attributes: dict)
```

- `name` indicates the name of a class
- `bases` is a tuple of classes to be inherited
- `attributes` is a dictionary including all variables and methods to be declared inside the new class

Example:

```python
Dummy = type("Dummy", (), {"var1": "lorem ipsum sit domat"})
dummy = Dummy()
print(dummy.var1)
```

Output:

```console
lorem ipsum sit domat
```

### 2. Creating Metaclass

To use class as a metaclass we pass `metaclass=ClassName` as a class parameter.

Example:

```python
class CustomMeta:
    def __new__(self, class_name, bases, attributes):
        print("Attributes received in CustomMeta:", attributes)
        return type(class_name, bases, attributes)

class Dummy(metaclass=CustomMeta):
    class_var1 = "lorem"
    class_var2 = 45
```

Output:

```console
Attributes received in CustomMeta: {'__module__': '__main__', '__qualname__': 'Dummy', 'class_var1': 'lorem', 'class_var2': 45}
```

Note that there’s output without creating an instance of the class because the `__new__()` method is called when a class is created.

Metaclasses should only be used when absolutely necessary, it is sometimes viewed as a bad practice.

### 3. Modifying a class state using Metaclass

Using Metaclasses, user can perform multitude of validations and modification such as changing variable names, raising error on receiving invalid data type, checking inheritance levels, etc.

For this example, we will write a Metaclass that raises a `ValueError` when a negative value is received in `attributes`.

```python
class CustomMeta:
    def __new__(self, class_name, bases, attributes):
        for attr, value in attributes.items():
            if type(value) in [int, float] and value < 0:
                raise ValueError(f"Negative values are not allowed in {class_name}")
        return type(class_name, bases, attributes)

class Dummy(metaclass=CustomMeta):
    class_var1 = 23
    class_var2 = -1

dummy = Dummy()
```

Output:

```console
Traceback (most recent call last):
  File "/home/user/meta.py", line 8, in <module>
    class Dummy(metaclass=CustomMeta):
  File "/home/user/meta.py", line 5, in __new__
    raise ValueError(f"Negative values are not allowed in {class_name}")
ValueError: Negative values are not allowed in Dummy
```
