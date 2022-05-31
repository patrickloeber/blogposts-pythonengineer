---
title: Enum in Python
date: 2022-05-18 00:00
description: Learn how to use Enum in Python.
tags: Python, Basics
path: enums-python
author: Shweta Goyal
---

Enum is a built-in data type in Python. It is used to create a finite set of constants.

Enum is a collection of symbolic names and values. It's a shortcut for enumeration and can be imported from the module `enum`.

Enumerations are created using classes.

Let's see an example to understand how to use enum in Python.

```python
from enum import Enum

class Birds(Enum):
    Crow = 1
    Eagle = 2
    Hawk = 3

# It can be displayed as string or repr
print(Birds.Crow) # Birds.Crow
print(repr(Birds.Crow)) # <Birds.Crow: 1>

# Checking the type of the enum
print(type(Birds.Crow)) # <enum 'Bird'>

# Checking the name of the enum using the `name` keyword
print(Birds.Crow.name) # Crow

# Checking the value of the enum using the `value` keyword
print(Birds.Crow.value) # 1
```

These are the properties of enum. It also supports iterations and can be iterated using loops. They are hashable and can be used as keys in dictionaries or as values in sets.

Let's understand more with examples.

```python
from enum import Enum

class Days(Enum):
    Monday = 1
    Tuesday = 2
    Wednesday = 3
    Thursday = 4
    Friday = 5
    Saturday = 6
    Sunday = 7

# Iterating over the enum and printing the members
print("Enum values are:")
for day in Days:
    print(day)

# Days.Monday
# Days.Tuesday
# Days.Wednesday
# Days.Thursday
# Days.Friday
# Days.Saturday
# Days.Sunday
```

For Hashing we use enum as dictionary keys:

```python
days_dict = {Days.Monday: "First day of the week", Days.Sunday: "Last day of the week"}

print(days_dict)
# {Days.Monday: 'First day of the week', Days.Sunday: 'Last day of the week'}

print(days_dict[Days(7)])
# Last day of the week

# or
print(days_dict[Days.Sunday])
# Last day of the week
```

Enum can be compared using the equality operator and identity operator. Let's see an example:

```python
from enum import Enum
class Days(Enum):
    Monday = 1
    Tuesday = 2
    Wednesday = 3

# Checking the equality operator
print(Days.Monday == Days.Monday) # True

# Checking the identity operator
print(Days.Monday is Days.Monday) # True

# Cannot compare the enum with other types
print(Days.Monday == 1) # False
```

## Conclusion

This is a basic tutorial on the enum in Python. Here, you have learned how to create an enum in Python and use it. You can learn more about enum in Python from the [Python documentation](https://docs.python.org/3/library/enum.html).
