---
title: How to write for loops in Python
date: 2021-07-21 00:00
description: A for loop is used for iterating over a sequence. This artice shows how to use for loops.
tags: Python, Basics
path: python-for-loops
author: Patrick Loeber
---

A for loop is used for iterating over a sequence. This can be for example a list, a tuple, a dictionary, a set, a string, or a range object.

To use a for loop we use the `for x in sequence` syntax.

With the for loop we can execute a set of statements, once for each item in the sequence.

```python
numbers = [1, 2, 3]
for x in fruits:
    print(x)
```

```
1
2
3
```

### Loop with the range function

To loop over numbers and use the current index, we can use the [range](https://docs.python.org/3/library/functions.html#func-range) function.
```python
for i in range(3):
    print(i)
```

```
0
1
2
```

Range can take only a stop argument, or a start and a stop argument. In the latter case it can also take an optional step argument:

- `range(stop)`
- `range(start, stop)`
- `range(start, stop, step)`

### Loop through a String

Looping through a string will go over each character.

```python
for x in "python":
    print(x)
```

```
p
y
t
h
o
n
```

### The break statement

The `break` statement can be used for an early stopping of the loop before it has looped through all the items. Typically this is applied when a certain condition is met.

```python
values = ["one", "two", "three"]
for value in values:
    print(x)
    if value == "two":
        break
```

```
one
two
```

### The continue statement
The `continue` statement is used to skip the current iteration.
```python
values = ["one", "two", "three"]
for value in values:
    if value == "two":
        continue
    print(x)
```

```
one
three
```

Note that here the print statement is applied at the end of each iteration, so after the possible `continue` statement.

### Advanced looping with enumerate
With `enumerate(x)` we can access both the index and the item:
```python
values = ["one", "two", "three"]
for idx, value in enumerate(values):
    print(idx, value)
```

```
0 one
1 two
2 three
```
