---
title: What is super() in Python
date: 2022-02-28 00:00
description: Learn the meaning of super and its usage with examples.
tags: Python, Basics
path: super-in-python
author: Pratik Choudhari
---

In Python, the super keyword is used to refer to the parent class. In this article we will understand the usage of `super()` and why it is required with examples.

## About super()

`super()` can only be used in a class that has been inherited from other classes. Its primary use is to access methods and variables of the parent classes without explicitly specifying the class name.

`super()` returns a proxy object which is a temporary object of the superclass, hence allowing the base class to refer to the superclass’s objects. When used inside `__init__()` we can call the parent class `__init__()` whenever the child class is initialized.

### MRO(Method Resolution Order)

MRO is a mechanism to resolve the method to be executed when super notation is used.

A common confusion occurs in case of multiple inheritance. What if a common method is implemented in multiple parents and it is called using super(), from which class should the method be called? This is determined by MRO and the order is easily accessible by executing

```python
ClassName.__mro__
```

## Usage

#### 1. Inside `__init__()`

```python
class Vehicle:
    def __init__(self, mode):
        self.mode = mode
        print(f"Mode of transportation: {self.mode}")


class Car(Vehicle):
    def __init__(self, model, make):
        super().__init__(mode="land")

        self.model = model
        self.make = make


Car("Volkswagen", "Polo")
```

Output:
```console
Mode of transportation: land
```

#### 2. Outside `__init__()`

```python
class Vehicle:
    def __init__(self, mode):
        self.mode = mode

    def print_mode(self):
        print(f"Mode of transportation: {self.mode}")


class Car(Vehicle):
    def __init__(self, model, make):
        super().__init__(mode="land")

        self.model = model
        self.make = make

    def print_all_info(self):
        super().print_mode()
        print(f"Model: {self.model} and make: {self.make}")


Car("Volkswagen", "Polo").print_all_info()
```

Output:
```console
Mode of transportation: land
Model: Volkswagen and make: Polo
```

To see the MRO of class `Car`

```python
print(Car.__mro__)
```

Output:

```console
(<class '__main__.Car'>, <class '__main__.Vehicle'>, <class 'object'>)
```

From this output, we understand that Python will first find the method in `Car` followed by `Vehicle` then `object`.