---
title: Deque in Python using Collections Module
date: 2022-06-01 00:00
description: Learn the basics of Deque in Python.
tags: Python, Basics
path: deque-python
author: Shweta Goyal
---

Deque is a double-ended queue. It can be used to add or remove elements from both the sides. In Python, we can use the collections.deque class to implement a deque.

The deque class is a general-purpose, flexible and efficient sequence type that supports **thread-safe, memory efficient appends and pops from either side**. A deque provides approximately **O(1) time complexity** for append and pop opeations in either direction.

There are various built-in functions available in the collections module to perform the operations on the deque. Let's see how to use them.

```python
from collections import deque

# Create a deque object
d = deque(['Black', 'White', 'Red', 'Green'])

# Add elements to the right side
d.append('Blue')
# deque(['Black', 'White', 'Red', 'Green', 'Blue'])

# Add elements to the left side
d.appendleft('Yellow')
# deque(['Yellow', 'Black', 'White', 'Red', 'Green', 'Blue'])

# Remove elements from the right side
d.pop()
# 'Blue'

# Remove elements from the left side
d.popleft()
# 'Yellow'

# Get the size of the deque
len(d)
# 5
```

In the above example, `append()` and `pop()` functions are used to add and remove elements from the right side of the deque. Similarly, `appendleft()` and `popleft()` functions are used to add and remove elements from the left side of the deque. `len()` function is used to get the size of the deque.

Let's see some more functions:

```python
from collections import deque

# Create a deque object
queue = deque(['Black', 'White', 'Red', 'Green'])

# Extend the right side of the deque
queue.extend(['Blue', 'Yellow'])
# deque(['Black', 'White', 'Red', 'Green', 'Blue', 'Yellow'])

# Extend the left side of the deque
queue.extendleft(['Orange', 'Purple'])
# deque(['Orange', 'Purple', 'Black', 'White', 'Red', 'Green', 'Blue', 'Yellow'])

# Count the number of times an element appears in the deque
queue.count('Black')
# 1

# Insert an element at a given index
queue.insert(2, 'Brown')
# deque(['Orange', 'Purple', 'Brown', 'Black', 'White', 'Red', 'Green', 'Blue', 'Yellow'])
```

In the above example, `extend()` and `extendleft()` functions are used to add multiple elements at the same time to the right and left sides of the deque. `count()` function is used to count the number of times an element appears in the deque. `insert()` function is used to insert an element at a given index.

## Conclusion

In this tutorial, we have learned the basics of Deque in Python using the collections module. We have also learned how to use the built-in functions available in the collections module to perform the operations on the deque. If you want to learn more about the deque class, you can refer to the [official documentation](https://docs.python.org/3/library/collections.html#collections.deque) of the collections module.
