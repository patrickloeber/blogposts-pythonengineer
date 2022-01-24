---
title: What are global, local, and nonlocal scopes in Python
date: 2022-01-25 00:00
description: Understand scopes and their usages with examples.
tags: Python, Basics
path: global-local-nonlocal-python
author: Pratik Choudhari
---

Scope is defined as an area where eligible variables can be accessed. To enforce security, programming languages provide means by which a user can explicitly define these scopes.

It is important to understand the use of scopes and how to deal with them. In this article, we will see what are the scopes available in Python and how to work with them.

## 1. Global scope

Any variable defined outside a non-nested function is called a global. As the name suggests, global variables can be accessed anywhere.

#### Example:

```python
side = 5 # defined in global scope

def area():
    return side * side

def circumference():
    return 4 * side

print(f"Area of square is {area()}")
print(f"Circumference of square is {circumference()}")
```

Output:

```console
Area of square is 25
Circumference of square is 20
```

When a function tries to manipulate global variables, an [UnboundLocalError](https://docs.python.org/3.3/library/exceptions.html#UnboundLocalError) is raised. To overcome this the global variable is redefined inside the function using  `global` keyword. In this way a user can modify global variables without errors.

#### Example:

Without global keyword

```python
side = 5

def multiply_side(factor):
  side *= factor

multiply_side(7)
print(f"Side length is {side}")
```

Output:

```console
UnboundLocalError: local variable 'side' referenced before assignment
```

With global keyword

```python
side = 5

def multiply_side(factor):
    global side
    side *= factor

multiply_side(7)
print(f"Side length is {side}")
```

Output:

```console
Side length is 35
```

## 2. Local scope

By default, variables defined inside a function have local scope. It implies that local scope variables can be accessed only inside the parent function and nowhere else.

Local variables are destroyed as soon as the scope ceases to exist.

#### Example:

```python
side = 5

def area():
    square_area = side * side # local scope

print(square_area)
```

Output:

```console
NameError: name 'square_area' is not defined
```

## 3. Nonlocal scope

Nested functions introduce a new type of scope called as `nonlocal` scope. 
When a nested function wants to share the local scope of parent functions, `nonlocal` keyword is used.

In such cases, declaring parent function variables as `global` does not work.

#### Example:

Without using `nonlocal` keyword

```python
side = 5

def half_area():
    area = side * side
    def divide():
        area /= 2

    divide()
    return area

print(half_area())
```

Output:

```console
UnboundLocalError: local variable 'area' referenced before assignment
```

Using `nonlocal` keyword:

```python
side = 5

def half_area():
    area = side * side
    def divide():
        nonlocal area
        area /= 2

    divide()
    return area

print(half_area())
```

Output:

```console
12.5
```

