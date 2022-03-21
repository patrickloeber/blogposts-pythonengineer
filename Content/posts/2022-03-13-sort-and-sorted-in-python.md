---
titlt: Difference between sort() and sorted() in Python
date: 2022-03-13 00:00
description: Learn the difference between sort() and sorted() function in Python
tags: Python Basic
path: 
author: Shweta Goyal
---

# Difference between sort() and sorted() in Python

Sorting any sequence in Python is easy as it provides built-in methods for sorting. Sorting means rearranging a given sequence of elements.

Python provides two built-in functions which are sort() and sorted(). These two functions are used for sorting but come with a few differences. Let’s see how you can use them.

## Python sort()

This function modifies the list in-place which means it modifies the original list and it has no return value. This method can be used only with lists as it is of the list class, it can not sort any other sequence like tuple, etc. This will sort the elements in ascending order by default.

Let’s see the syntax:

`list_name.sort(key, reverse=False)`

It consists of two parameters and they both are optional:

**key:** It is a function that specifies the sorting criteria.
**reverse:** It is False by default which sort in ascending order. If it is true, it will sort the elements in descending order.

Let’s go through some examples which will help you to understand more:

Example 1: Without any parameter

```python

## Without Any Parameters

colors = ['Black', 'Purple', 'Green', 'Yellow', 'Orange']
colors.sort()
print("Sorted list:", colors)

## Output: 
Sorted list: ['Black', 'Green', 'Orange', 'Purple', 'Yellow']
```

By default, it is sorting the elements in ascending order. Let’s sort the element in descending order.

Example 2: With the `reverse` argument

```python

## With the reverse argument

colors = ['Black', 'Purple', 'Green', 'Yellow', 'Orange']
colors.sort(reverse=True)
print("Sorted list (in descending):", colors)

## Output:
Sorted list (in descending): ['Yellow', 'Purple', 'Orange', 'Green', 'Black']
```

The list is sorted in descending order now. Let’s sort the element using a key argument.

Example 3: With the ‘key’ argument

```python

## With the key argument

def length(color):
    return len(color)

colors = ['Black', 'Purple', 'Green', 'Yellow', 'Orange']

colors.sort(key=length)
print("Sorted list:", colors)

colors.sort(key=length, reverse=True)
print("Sorted list (in descending):", colors)

## Output:
Sorted list: ['Black', 'Green', 'Purple', 'Yellow', 'Orange']
Sorted list (in descending): ['Purple', 'Yellow', 'Orange', 'Black', 'Green']
```

The list is sorted in ascending as well as in descending order according to the function which calculates the length of the elements.

## Python sorted()

This function does not change the original list and returns a sorted list. This method can be used on any sequence like list, tuple, string, or any iterable that you want to be sorted. This will sort the elements in ascending order by default.

Let’s see the syntax:

`sorted(iterable, key, reverse=False)`

It consists of three parameters and two are optional:

**iterable:** It can be a sequence like a list, tuple, string, or collection like a set, dictionary, etc., or any other iterator.
**key:** It is a function that specifies the sorting criteria. It is an optional argument.
**reverse:** It is False by default which sort in ascending order. If it is true, it will sort the elements in descending order. It is an optional argument.

Let’s go through some examples which will help you to understand more:

Example 1: With iterable argument

```python

## With iterable argument

colors = ('Black', 'Purple', 'Green', 'Yellow', 'Orange')
print("Sorted list:", sorted(colors))

## Output:
Sorted list: ['Black', 'Green', 'Orange', 'Purple', 'Yellow']
```

The iterator is a tuple and the sorted function returns a sorted list. By default, it is sorting the elements in ascending order. Let’s sort the element in descending order.

Example 2: With the `reverse` argument

```python

## With the reverse argument

colors = ('Black', 'Purple', 'Green', 'Yellow', 'Orange')
print("Sorted list (in descending):", sorted(colors, reverse=True))

## Output:
Sorted list (in descending): ['Yellow', 'Purple', 'Orange', 'Green', 'Black']
```

The list is sorted in descending order now. Let’s sort the element using a key argument.

```python

## With the key argument

def length(color):
    return len(color)

colors = ('Black', 'Purple', 'Green', 'Yellow', 'Orange')

print("Sorted list:", sorted(colors, key=length))

print("Sorted list (in descending):", sorted(colors, key=length, reverse=True))

## Output:
Sorted list: ['Black', 'Green', 'Purple', 'Yellow', 'Orange']
Sorted list (in descending): ['Purple', 'Yellow', 'Orange', 'Black', 'Green']
```

The list is sorted in ascending as well as in descending order according to the function which calculates the length of the elements.

**Note:** sorted() function creates a copy of the object during sorting which creates additional overhead compared to the sort() function. Hence, the sort() function is faster than the sorted() function.

## Conclusion

This article helps you to understand the differences and the similarities between the sort() and the sorted() function. You can use the sort() function for faster operation and if you want to mutate or change the list otherwise use the sorted() function.
