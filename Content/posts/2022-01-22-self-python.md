---
title: What is self in Python classes
date: 2022-01-24 00:00
description: Learn how class states are controlled and tracked using a single word.
tags: Python, Basics
path: self-python
author: Pratik Choudhari
---

In object-oriented programming, a class is a template that defines methods and variables common to all objects of a certain kind. The *self* word in Python **refers to an instance of a class**, it is not a keyword and can be replaced by any other name.

Instance methods inside a class have to use *self* as first argument. It helps the methods to track of and manipulate the class state. As self refers to a class instance, different class instances can have different states such as variable values.

Note that when calling instance methods on an object, *self* is not used!

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

    def set_age(self, age):
        self.age = age

p = Person("Ross", 30)
print(p.fetch_name())
print(p.fetch_age())

p.set_age(31)  # no self here!
print(p.fetch_age())
```

Output:
```console
'Ross'
30
31
```

## Manipulating instance variables

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

## Using another name instead of self

Surprisingly, *self* could be replaced by any other name irrespective of method.

But while this is technically possible, the convention is to always call this *self*.

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
'Ross'
30
```
