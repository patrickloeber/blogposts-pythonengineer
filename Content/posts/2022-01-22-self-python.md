---
title: What is self in Python classes
date: 2022-01-22 00:00
description: Learn how class states are controlled and tracked using a single word.
tags: Python, Basics
path: self-python
author: Pratik Choudhari
---

In object-oriented programming, a class is a template that defines methods and variables common to all objects of a certain kind. 
The self word in python refers to an instance of a class, it is not a keyword and can be replaced by any other name. 
Methods inside a class are forced to take self as an argument, it helps the methods to track of and manipulate the class state. 
As self refers to a class instance, different class instances can have different states such as variable values.

Example:
```python
class Person:
  def __init__(self, name, age):
    self.name = name
    self.age = age
  def fetch_name(self):
    return self.name
  def fetch_age(self):
    return self.age

p = Person("Ross", 30)
print(p.fetch_name())
print(p.fetch_age())
```

Output:
```console
'Ross'
30
```

### Manipulating instance variables

Instance variables are defined in the `__init__()` method also known as the class constructor. These variables can be accessed via the class instance object.

Example:
```python
p = Person("Joey", 29)
print(p.name)
p.name = "Jim"
print(p.name)
```

Output:
```console
'Joey'
'Jim'
```

### Using another name instead of self

Surprisingly, the self can be replaced by any other name irrespective of method, as the first argument should always be a reference to the instance.

Example:
```python
class Person:
  def __init__(first_self, name, age):
    first_self.name = name
    first_self.age = age
  def fetch_name(second_self):
    return second_self.name
  def fetch_age(third_self):
    return third_self.age

p = Person("Ross", 30)
print(p.fetch_name())
print(p.fetch_age())
```

Output:
```console
'Joey'
30
```
