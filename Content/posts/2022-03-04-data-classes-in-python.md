---
title: Data classes in Python with dataclass decorator
date: 2022-03-09 00:00
description: Learn the basics of data classes in Python using the dataclasses module and the dataclass decorator with all possible parameters.
tags: Python, Basics
path: dataclass-python
author: Shweta Goyal
---

Learn the basics of data classes in Python using the `dataclasses` module and the `dataclass` decorator with all possible parameters.

Data classes are regular classes that are geared towards storing state, rather than containing a lot of logic. If you need a class that mostly consists of attributes, and don't need a lot of methods, you can make a data class.

The [dataclasses module](https://docs.python.org/3/library/dataclasses.html) makes it easier to create data classes since it takes care of a lot of boilerplate for you. It provides the `dataclass` decorator that automatically adds [special methods](https://docs.python.org/3/glossary.html#term-special-method) such as `__init__()` and `__repr__()` to user-defined classes.

Moreover, it offers some additional functions that are handy when working with a dataclass.

## A regular class without dataclass

First, let's see a regular class. Here, we have to implement all methods ourselves to get the behavior we want:

```python
class Student:
    def __init__(self, id, name):
        # Instance variables
        self.id = id
        self.name = name

    def __repr__(self):
        return ("Student Info: id={}, name={}".format(self.id, self.name))

student = Student(22, "Paul")
print(student)
```

Output:

```console
Student Info: id=22, name=Paul
```

Now let's see how we can achieve the same behaviour with much less code using `dataclass`.

## An example using `dataclass`

Let’s implement the same class using the `dataclass` decorator:

```python

from dataclasses import dataclass


@dataclass
class Student:
    id: int
    name: str


student = Student(22, "Paul")
print(student)
```

Output:

```console
Student(id=22, name='Paul')
```

Here, we don’t have to define separate functions like `__init__()` and `__repr__(), since the `dataclass` decorator will add this for us.


## Default Values in Data Classes

You can assign default values to your fields. Then we don't have to use them in the constructor. Let’s see an example:

```python
from dataclasses import dataclass


@dataclass
class Student:
    id: int 
    name: str = "John"


student = Student(22)
print(student)
```

Output:

```console
Student(id=22, name='John')
```

Note: Default values attributes must appear after the ones without default values, otherwise you will get an error.

## Immutable/Frozen Data Classes

Immutable objects mean you can’t change the values of attributes after it is created. They are read-only objects.

You have to set the `frozen` parameter from the `dataclass` decorator to True to make the data class immutable. By default, data classes are mutable.

Let’s see an example:

```python

from dataclasses import dataclass

@dataclass(frozen=True)
class Student:
    id: int 
    name: str = "John"


student = Student(22, "Paul")
student.id = 20
```

This will raise a `FrozenInstanceError`:

```console
dataclasses.FrozenInstanceError: cannot assign to field 'id'
```

In the example above, if you change the value of the attribute after setting the frozen parameter to True, you will get an error.

## Conversion to a tuple or a dictionary

There are two functions in the data class module which are `astuple()` and `asdict()` and they convert a data class instance to a tuple or a dictionary. Let's see an example:

```python

from dataclasses import dataclass, astuple, asdict

@dataclass
class Student:
    id: int 
    name: str 


student = Student(22, "Paul")

print("Tuple:", astuple(student))
print("Dictionary:", asdict(student))
```

Output:

```console
Tuple: (22, 'Paul')
Dictionary: {'id': 22, 'name': 'Paul'}
```

## Full dataclass syntax and optional parameters

The full dataclass decorator can have these optional arguments:

```python
dataclass(*, init=True, repr=True, eq=True,
             order=False, unsafe_hash=False, frozen=False,
             match_args=True, kw_only=False, slots=False)
```

`*` here means that all arguments must be passed as keyword arguments. Let's look at the different arguments in detail:

- `init`: This is for initialization. It is True by default and it will be generated automatically. If the class defines it explicitly then this method will be ignored.

- `repr`: This is for the representation of string objects and they are returned in the order they are defined. It is True by default and it will be generated automatically. If the class defines it automatically then this method will be ignored.

- `eq`: This is for the equality between two objects and it checks if the two objects have the same data. It is True by default and it will be generated automatically. If the class defines it automatically then this method will be ignored.

- `order`: This is for the comparison and if it is True then it will generate the methods `__lt__()`, `__le__()`, `__gt__()`, and `__ge__()`. This is False by default.

- `unsafe_hash`: If it is False then it will generate `__hash__()` method according to how `eq` and `frozen are set. This is False by default.

- `frozen`: If it is True then it will generate an exception when assigned to fields. This is False by default.

Note: If the `order` is True then `eq must be True, otherwise you will get a ValueError.

To read about the other arguments, you can have a look at the [official documentation](https://docs.python.org/3/library/dataclasses.html#dataclasses.dataclass).

## Conclusion

In this article, you have learned about the data classes and how they can make your code more readable. This is a beginner-friendly article and there are so many things that you can learn and implement. You can get more information from their [official site](https://docs.python.org/3/library/dataclasses.html).
