---
title: How to use pprint in Python?
date: 2022-05-15 00:00
description: Exploring the pprint library using explainations and examples
tags: Python, Basics
path: pprint-python
author: Pratik Choudhari
---

[`pprint`](https://docs.python.org/3/library/pprint.html) is used to print a beautified representation of an object in Python. It is available as a standard library that comes preinstalled with Python interpreter. This article will explore how `pprint` is used and what formatting options it provides.

## 1. pprint.pprint(object)

This is the most famous function from the `pprint` module, it passes the arguments and keyword arguments to the `PrettyPrinter` class constructor. Following are the arguments accepted by the function:

- object: Python object to print
- indent: The amount of indentation to use in every new nesting level
- width: Maximum number of characters that can be printed in a line
- depth: Specifies the number of nesting levels to print, after the depth is surpassed `...` characters are printed
- sort_dicts: Sort dictionaries based on keys
- underscore_numbers: Add `_` separator to every thousandths place in a number
- compact: If true, adjust items of a sequence in the width else print each element in a new line
- stream: Stream to which data is to be sent like `StringIO` or `BytesIO`, defaults to `sys.stdout`

Example:

```python
from pprint import pprint

nested_dict = [{"language": "Python", "application": ["Data Science", "Automation", "Scraping", "API"]}, {"language": "Javascript", "application": ["Web Development", "API", "Web Apps", "Games"]}]

pprint(nested_dict, indent=3) # 2 extra indents while printing dictionary
```

Output:

```console
[  {  'application': ['Data Science', 'Automation', 'Scraping', 'API'],
      'language': 'Python'},
   {  'application': ['Web Development', 'API', 'Web Apps', 'Games'],
      'language': 'Javascript'}]
```

## pprint.pformat(object)

`pformat()` is similar to `pprint()`, the distinctions are:

- pprint sends formatted data to a stream whereas pformat() returns a string with formatted data
- pformat does not take stream argument, all other arguments remain as they were

Example:

```python
from pprint import pformat

nested_dict = [{"language": "Python", "application": ["Data Science", "Automation", "Scraping", "API"]}, {"language": "Javascript", "application": ["Web Development", "API", "Web Apps", "Games"]}]

string_representation = pformat(nested_dict)
print(string_representation)
```

Output:

```console
[{'application': ['Data Science', 'Automation', 'Scraping', 'API'],
  'language': 'Python'},
 {'application': ['Web Development', 'API', 'Web Apps', 'Games'],
  'language': 'Javascript'}]
```

## pprint.pp(object)

Alias to `pprint.pprint()`, available from Python 3.8 and above.

## pprint.isreadable(object)

Returns True if the object passed is readable by pprint, if an object is readable it can be pretty printed.

## pprint.isrecursive(object)

Returns True if the object passed has recursive structure.

Example:

```python
from pprint import pprint, isrecursive

recursive_dict = {}
recursive_dict[0] = recursive_dict[1] = recursive_dict

print(isrecursive(recursive_dict))
pprint(recursive_dict)
```

Output:

```console
True
{0: <Recursion on dict with id=140056761037664>,
 1: <Recursion on dict with id=140056761037664>}
```
