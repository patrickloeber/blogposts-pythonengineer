---
title: What are metaclasses in Python
date: 2022-02-07 00:00
description: A beginners guide to metaclasses in Python.
tags: Python, Basics
path: metaclasses-python
author: Pratik Choudhari
---

Metaclass is an advanced Python concept and is not used in day-to-day programming tasks. They allow a user to precisely define a class state, change its attributes and control method behavior.

In this article, we will understand how metaclasses can be created and used in Python.

## 1. Type and OOP

Everything is an object in Python, including classes. Hence, if classes are an object, they must be created by another class also called as Metaclass.

![class hierarchy](/images/2022-01-29-metaclasses/metaclass.webp)

So, a metaclass is just another class that creates class objects. Usually, `type` is the built-in metaclass Python uses for every class. But we can also create our own metaclasses with custom behavior.

## 2. Understanding the `type()` function

To fully understand Metaclasses, one needs to thoroughly understand `type()`.

In Python, `type()` is used to identify the data type of a variable. If we have the following code

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

Here, we can see `foo_obj` is correctly identified as an instance of class `Foo`, but the type of class `Foo` indicates that it is an instance of class `type`, establishing the point that classes are indeed created by other classes.

## Creating classes dynamically using `type()`

This is one more concept we should know before diving into metaclasses.

This usage of `type()` is fairly unknown. The `type()` function can take three arguments and can be used to create classes dynamically:

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

## 3. Creating Metaclass

The main purpose of a metaclass is to change the class automatically when it's created.

To use class as a metaclass we pass `metaclass=ClassName` as a class parameter. The metaclass itself is implemented like a normal class with any behavior we want. Usually the `__new__` function is implemented.

The name of the metaclass should ideally make the intent of the class clear:

Example:

```python
class PrintAttributeMeta:
    def __new__(cls, class_name, bases, attributes):
        print("Attributes received in PrintAttributeMeta:", attributes)
        return type(class_name, bases, attributes)

class Dummy(metaclass=PrintAttributeMeta):
    class_var1 = "lorem"
    class_var2 = 45
```

Output:

```console
Attributes received in PrintAttributeMeta: {'__module__': '__main__', '__qualname__': 'Dummy', 'class_var1': 'lorem', 'class_var2': 45}
```

This meta class simply prints all attributes, and then creates and returns a new class by using the `type()` function.

Note that there’s output without creating an instance of the class because the `__new__()` method is called when the class is created.

## 4. Modifying a class state using Metaclass

Using Metaclasses, the user can perform multitude of validations and modification such as changing variable names, raising error on receiving an invalid data type, checking inheritance levels, etc.

For this example, we will write a Metaclass that raises a `ValueError` when a negative value is received in `attributes`.

```python
class PositiveNumbersMeta:
    def __new__(cls, class_name, bases, attributes):
        for attr, value in attributes.items():
            if isinstance(value, (int, float)) and value < 0:
                raise ValueError(f"Negative values are not allowed in {class_name}")
        return type(class_name, bases, attributes)

class MyClass(metaclass=PositiveNumbersMeta):
    class_var1 = 23
    class_var2 = -1
```

Output:

```console
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 5, in __new__
ValueError: Negative values are not allowed in MyClass
```

We could also change attributes:

```python
class PositiveNumbersMeta:
    def __new__(cls, class_name, bases, attributes):
        for attr, value in attributes.items():
            if isinstance(value, (int, float)) and value < 0:
                attributes[attr] = -value
        return type(class_name, bases, attributes)

class MyClass(metaclass=PositiveNumbersMeta):
    class_var1 = 23
    class_var2 = -1

a = MyClass()
print(a.class_var2)  # 1
```

## 5. Use proper OOP principles

In the previous example we are calling `type` directly and aren't overriding or calling the parent's `__new__`. Let's do that instead:

```python
class PositiveNumbersMeta(type):
    def __new__(cls, class_name, bases, attributes):
        for attr, value in attributes.items():
            if isinstance(value, (int, float)) and value < 0:
                attributes[attr] = -value
        return super.__new__(class_name, bases, attributes)
```

Now our metaclass inherits from `type`, and by calling the `super.__new__()` we are using the OOP syntax and call the `__new__()` function of the base class.

## 6. When to use metaclasses?

There are several reasons to do so:

* The intention is clear. When you read PositiveNumbersMeta, you know what's going to follow
* You can use OOP. Metaclass can inherit from metaclass, override parent methods, etc. Metaclasses can even use other metaclasses.
* You can structure your code better. You never use metaclasses for something as trivial as the above example. It's usually for something complicated. Having the ability to make several methods and group them in one class is very useful to make the code easier to read.
* You can hook on `__new__`, `__init__` and `__call__`. Which will allow you to do different stuff, Even if usually you can do it all in `__new__`, some people are just more comfortable using `__init__`.

Resource: Here's a great [StackOverflow answer](https://stackoverflow.com/questions/100003/what-are-metaclasses-in-python) that explains it well.

Note that Metaclasses are usually only used in more complex scenarios, and in 99% of cases you don't have to worry about it. One common use case is when creating an API. A typical example of this is the [Django ORM](https://docs.djangoproject.com/en/4.0/topics/db/models/).
