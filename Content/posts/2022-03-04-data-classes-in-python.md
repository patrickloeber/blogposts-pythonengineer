---
titlt: Dataclasses in Python
date: 2022-03-04 00:00
description: Learn the basics of dataclasses in Python
tags: Python, Basics
path: dataclass-python
author: Shweta Goyal
---

[Dataclasses](https://docs.python.org/3/library/dataclasses.html) are a bit different from Python classes because Python classes encapsulate data and functions together but Data classes focus more on data rather than the functionality part. Data classes come with [decorator](https://wiki.python.org/moin/PythonDecorators#:~:text=A%20decorator%20is%20the%20name,of%20the%20function%20being%20decorated.) and functions that automatically adds generated [special methods](https://docs.python.org/3/glossary.html#term-special-method) such as __init__() and __repr__() to user-defined classes. These classes help to reduce boilerplate code and more functionality.

Let’s see a regular example without data class:

```python

# Student class
class Student:

    # Initialization (init method)
    def __init__(self, id, name):

        # Instance variables
        self.id = id
        self.name = name

    # Return class objects
    def __repr__(self):
        return ("Student Info: id={}, name={}".format(self.id, self.name))

Stu = Student(22, "Paul")
print(Stu)

# Output:
Student Info: id=22, name=Paul
```

Here, there are two functions and each time you pass an argument, it copies its properties and then returns the object. It works for small data but if you have large data then it will make your code messy and complicated. So, that’s why data classes exist, to make your code readable and easy.

Data Classes have inbuilt constructors like __init__(), __repr__(), etc that will handle everything automatically like the data and the object creation. Let's see the syntax:

`dataclass(*, init=True, repr=True, eq=True, order=False, unsafe_hash=False, Frozen=False)`

The parameter values are in boolean which are the default values and they indicate whether the respective method will be generated or not. * here means other methods but these are the most common. Let's discuss parameters:

1. __init__: This is for initialization. It is True by default and it will be generated automatically. If the class defines it explicitly then this method will be ignored.

2. __repr__: This is for the representation of string objects and they are returned in the order they are defined. It is True by default and it will be generated automatically. If the class defines it automatically then this method will be ignored.

3. __eq__: This is for the equality between two objects and it checks if the two objects have the same data. It is True by default and it will be generated automatically. If the class defines it automatically then this method will be ignored.

4. __order__: This is for the comparison and if it is true then the methods will be generated are __lt__(), __le__(), __gt__(), and __ge__(). This is False by default.

5. __unsafe_hash__: If it is False then it will generate __hash__() method according to how eq and frozen are set. This is False by default.

6. __Frozen__: If it is True then it will generate an exception when assigned to fields. This is False by default.

Note: If the __order__ is True then __eq__ must be True, otherwise you will a ValueError.

Let’s implement an example with data classes.

```python

from dataclasses import dataclass

# Class for holding content
@dataclass
class Student:

    # Declaring attributes
    id: int
    name: str

# Object of the class
Stu = Student(22, "Paul")
print(Stu)

# Output:
Student(id=22, name='Paul')
```

Here, we don’t have to define separate functions like __init__() and __repr__().

## Default Values

You can assign default values to your fields. Let’s see an example:

```python
from dataclasses import dataclass

# Class for holding content
@dataclass
class Student:

    # Declaring attributes
    id: int 
    name: str = "John"

# Object of the class
Stu = Student(22)
print(Stu)

#Output:
Student(id=22, name='John')
```

Note: Default values attributes must appear after the ones without default values, otherwise you will get an error.

## Immutable Objects

Immutable objects mean you can’t change the values of attributes after it is created. They are read-only objects. You have to set the frozen parameter from the data class decorator to True to make the data class immutable. By default, data classes are mutable. Let’s see an example:

```python

from dataclasses import dataclass

# Class for holding content
@dataclass(frozen=True)
class Student:

    # Declaring attributes
    id: int 
    name: str = "John"

# Object of the class
Stu = Student(22, "Paul")
Stu.id = 20

# Error:
dataclasses.FrozenInstanceError: cannot assign to field 'id'
```

In the example, If you change the value of the attribute after setting the frozen parameter to True, you will get an error.

## Conversion to a tuple or a dictionary

There are two functions in the data class module which are astuple() and asdict() and they convert a data class instance to a tuple or a dictionary. Let's see an example:

```python

from dataclasses import dataclass, astuple, asdict

# Class for holding content
@dataclass
class Student:

    # Declaring attributes
    id: int 
    name: str 

# Object of the class
Stu = Student(22, "Paul")

print("Tuple:", astuple(Stu))
print("Dictionary:", asdict(Stu))

# Output:
Tuple: (22, 'Paul')
Dictionary: {'id': 22, 'name': 'Paul'}
```

## Conclusion

In this article, you have learned about the data classes and how they can make your code more readable. This is a beginner-friendly article and there are so many things that you can learn and implement. You can get more information from their [official site](https://docs.python.org/3/library/dataclasses.html).
