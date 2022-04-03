---
title: Difference between set() and frozenset() in Python
date: 2022-04-05 00:00
description: Learn the difference between set() and frozenset() function in Python.
tags: Python, Basics
path: set-vs-frozentset
author: Shweta Goyal
---

Python provides two built-in functions which are set() and frozenset(). These two functions are used for creating sets but come with a few differences. Let’s see how you can use them.

## Python set()

A set is an unordered and unindexed collection of unique elements. Sets are mutable, you can change the elements using a built-in function like add(), remove(), etc. Since the elements are mutable and not in order, they don’t have hash values. So you can’t access the elements with the help of index numbers.

**Note:** Sets can’t be used as a dictionary key or as elements of another set. They can be used as a dictionary value.

Set is represented by curly braces like this `{}` or you can use `set()`. You can’t use only curly braces to create an empty set, this will create a dictionary. You can use `set()` if you want to create an empty set. Sets can include any immutable data type like string, number, tuple, etc. You can also include mutable data type like list, dictionary, etc.

Let’s go through some examples and see some of the operations you can perform on sets:

```python
fruits = {"Apple", "Banana", "Cherry", "Apple", "Kiwi"}

print('Unique elements:', fruits)

# Add new fruit
fruits.add("Orange")
print('After adding new element:', fruits)

# Size of the set
print('Size of the set:', len(fruits))

# check if the element is present in the set
print('Apple is present in the set:', "Apple" in fruits)
print('Mango is present in the set:', "Mango" in fruits)

# Remove the element from the set
fruits.remove("Mango")
print('After removing element:', fruits)

# Discard the element from the set
fruits.discard("Mango")
print('After discarding element:', fruits)
```

The output of the above code is as follows:

```console
Unique elements: {'Kiwi', 'Apple', 'Cherry', 'Banana'}
After adding new element: {'Kiwi', 'Orange', 'Banana', 'Apple', 'Cherry'}
Size of the set: 5
Apple is present in the set: True
Mango is present in the set: False
Traceback (most recent call last):
  File "c:\Users\hp\Desktop\set() and frozenset().py", line 19, in <module>
    Fruits.remove("Mango")
KeyError: 'Mango'
```

In the above example, some of the built-in functions have been used. There exists two functions `remove()` and `discard()` which help to remove the element from the set. They both remove the element from the set if there is an element present in the set but there is a difference between them.  

If the element is not in the set which you want to remove then `discard()` returns none while `remove()` will raise an error. You can learn more about the operations from their [official documentation](https://docs.python.org/3/library/stdtypes.html#set).

## Python frozenset()

A frozenset is an unordered and unindexed collection of unique elements. It is immutable and it is hashable. It is also called an immutable set. Since the elements are fixed, unlike sets you can't add or remove elements from the set.

Frozensets are hashable, you can use the elements as a dictionary key or as an element from another set. Frozensets are represented by the built-in function which is `frozenset()`. It returns an empty set if there are no elements present in it. You can use `frozenset()` if you want to create an empty set.

Let's go through some examples to understand more about frozenset:

```python
fruits = {"Apple", "Banana", "Cherry", "Apple", "Kiwi"}
basket = frozenset(fruits)

print('Unique elements:', basket)

# Add new fruit throws an error!
basket.add("Orange")
print('After adding new element:', basket)
```

The output of the above code is as follows:

```console
Unique elements: frozenset({'Kiwi', 'Cherry', 'Apple', 'Banana'})
Traceback (most recent call last):
  File "c:\Users\hp\Desktop\set() and frozenset().py", line 37, in <module>
    Basket.add("Orange")
AttributeError: 'frozenset' object has no attribute 'add'
```

The above example shows you can't add a new element to the frozenset.

Let's see how can use a dictionary with frozenset:

```python
student = {"Name": "John", "Age": "25", "Gender": "Male"}
key = frozenset(student)

print("The keys are:", key)
```

Output:

```console
The keys are: frozenset({'Age', 'Name', 'Gender'})
```

Let's see other operations that you can perform on frozenset, you can also perform these operations on normal sets:

```python
numbers1 = frozenset([1, 2, 3, 4, 5])
numbers2 = frozenset([2, 3, 4, 5])

# Combining both of them using "|" operator
# You can also use union() method
combined = numbers1 | numbers2
print("Combined set:", combined)

# Selecting common elements using "&" operator
# You can also use intersection() method
intersect = numbers1 & numbers2
print("Intersected set:", intersect)

# Selecting elements which are not common using "-" operator
# You can also use difference() method
difference = numbers1 - numbers2
print("Difference set:", difference)

# Membership testing

# It returns True if sets (frozenset) have no common items otherwise False
Disjoint = numbers1.isdisjoint(numbers2)
print("Disjoint:", Disjoint)

# It returns True if all the items of a set (frozenset) are common in another set (frozenset)
Subset = numbers1.issubset(numbers2)
print("Subset:", Subset)

# It returns True if a set (frozenset) has all items present in another set (frozenset)
Superset = numbers1.issuperset(numbers2)
print("Superset:", Superset)
```

The output of the above code is as follows:

```console
Combined set: frozenset({1, 2, 3, 4, 5})
Intersected set: frozenset({2, 3, 4, 5})
Difference set: frozenset({1})
Disjoint: False
Subset: False
Superset: True
```

You can learn more about the operations from their [official documentation](https://docs.python.org/3/library/stdtypes.html#frozenset).

## Conclusion

So far we have learned about sets and frozensets. We have also learned about the operations that you can perform on sets and frozensets. We have also learned about the difference between sets and frozensets. You can learn more about them from their [official documentation](https://docs.python.org/3/library/stdtypes.html#set-types-set-frozenset).
