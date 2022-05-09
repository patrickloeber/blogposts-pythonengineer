---
title: Working with Stacks in Python
date: 2022-05-09 03:00
description: This article explains the definition of stacks and how to create/use them.
tags: Python, Basics, Data Structures
path: python-stacks
author: Soham Datta
---

A stack is a linear data structure which follows a particular order in which the data operations are performed. This article explains the definition of stacks and how to create/use them.

## What are Stacks?

There are many type of data structures that we can use in Python. One such data structure is a stack.

Stacks can be thought as a pile of books on top of another. Imagine you want to add a book to the pile.

The simplest way to do this is to place the book on top of the top-most book of the pile.

Now imagine, you want to remove a book from the pile. Notice, that you can only remove the book from the top of the pile.

This is the fundamental principal of stacks. We name the order of adding/removing elements into a stack as **LIFO (Last In First Out)** or FILO (First In Last Out).

**A stack has a fixed length**. This means there is a maximum number of elements that can be inserted into a stack.

- If we try to add more elements to a stack than it's fixed length, we get a **"OVERFLOW"**
- Similarly, if we try to remove an element from an empty stack, we get an **"UNDERFLOW"**

Also, the type of elements is fixed in a stack. This means you cannot add an integer and a string to the same stack.

Think of this as keeping your Maths books in the pile of your computer books! What a mess! 

## Creating Stacks in Python

Unfortunately we don't have stacks as a built-in data type in Python.

However, it's quite simple to design our own stack object using Python's *Object Oriented Programming*.

We will be utilizing Python's list type data stucture to implement our stacks. 

```python
class Stack:
    """
    This class can be used to understand the basic concepts
    of Stack data structures and perform simple operations.

    Methods Available:
    (i) push    (ii) pop    (iii) peek    (iv) show
    """
    __status__ = {                  # Some status codes
       -2:"ERROR - TYPE-MISMATCH", 
       -1:"ERROR - UNDERFLOW",
        0:"ERROR - OVERFLOW",
        1:"DONE",
    }
    
    def __init__(self, size:int, _class:type):
        self.stack = [] # Our empty stack
        self.size = size # Size of our stack
        self.type = _class
        
    def push(self, element) -> int:
        # Inserts an element to the top of the stack
        if not isinstance(element, self.type):
            return Stack.__status__[-2]
        elif self.size < len(self.stack) + 1:
            return Stack.__status__[0]
        else:
            self.stack.append(element)
            self.element = element
            return Stack.__status__[1]

    def pop(self) -> int:
        # Removes the top-most element
        if len(self.stack) == 0:
            return Stack.__status__[-1]
        else:
            self.stack = self.stack[:-1]
            if len(self.stack) == 0:
                self.element = None
            else:
                self.element = self.stack[-1]
            return Stack.__status__[1]

    def peek(self):
        # Returns the top-most element
        if len(self.stack) == 0:
            return None
        else:
            return self.element
    
    def show(self) -> list | None:
        # Returns the entire stack
        if len(self.stack) == 0:
            return None
        else:
            return self.stack
```

## Working with Stacks

Now that we have created our *stacks* object, let's see how to use them.

First, let's create a stack of length 5 and data type integers.

```python
stack = Stack(size=5, _class=int)
```

Now, let's add some data into the stack.

```python
>>> stack.push(36)
'DONE'
>>> stack.push(67)
'DONE'
>>> stack.show()
[36, 67]
```

Now, let's try to remove some elements from the stack.

```python
>>> stack.pop()
67
>>> stack.pop()
36
>>> stack.pop()
'ERROR - UNDERFLOW'
```

Let's see what happens if we try to add more than 5 elements to the stack.

```python
>>> stack.push(17)
'DONE'
>>> stack.push(25)
'DONE'
>>> stack.push(74)
'DONE'
>>> stack.push("Python")
'ERROR - TYPE-MISMATCH'
>>> stack.peek()
74
>>> stack.push(49)
'DONE'
>>> stack.push(52)
'DONE'
>>> stack.push(93)
'ERROR - OVERFLOW'
>>> stack.show()
[17, 25, 74, 49, 52]
```

This is how we can create stacks in Python. Hope this helps!
