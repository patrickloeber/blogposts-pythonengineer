---
title: How to slice sequences in Python
date: 2022-01-13 00:00
description: Learn slicing with its variations and examples.
tags: Python, Basics
path: sequence-slicing
author: Pratik Choudhari
---

Slicing of sequences in Python is a crucial and easy to learn concept. In this article we will see different types of slicing and understand them with examples.

## About Sequences

Sequence data structures are iterable and the elements of a sequence can be accessed via their index except `set` and `frozenset`.

Slicing relies on indexing to specify the portion of sequence to extract data from.

As slicing is allowed only for indexable sequences the following data structures are eligible:

- list
- tuple
- bytearray
- string
- range
- byte sequences

## The Slice Notation:

```python
my_list[start: end: step]
```

Alternatively, `slice()` can be used 

```python
my_list[slice(start, end, step)]
```

Here, `start`, `end` and `step` are integers. `start` defines the index to start slicing from and continue till index `end - 1`(end index is excluded).

There are multiple variations of using slice notation:

- `[:, end]`: Select portion from sequence start till `end - 1`
- `[start: ]`: Select portion from start till the end of sequence
- `[:]`: Create a copy of sequence

Examples:

### 1. With start and end
```python
colors = ["red", "green", "blue", "yellow", "cyan"]
print(colors[1: 3])
```

Output:
```console
['green', 'blue']
```

### 2. With end only
```python
colors = ["red", "green", "blue", "yellow", "cyan"]
print(colors[: 4])
```

Output:
```console
['red', 'green', 'blue', 'yellow']
```

### 3. With start only
```python
colors = ["red", "green", "blue", "yellow", "cyan"]
print(colors[2:])
```

Output:
```console
['blue', 'yellow', 'cyan']
```


## The `step` in Slicing
`step` defines the number of index to move forward while slicing an object. If `step` is not specified, default value is taken as 1 which means move without skipping any index.

Example:
```python
colors = ["red", "green", "blue", "yellow", "cyan"]
print(colors[: 4: 2])
```

Output:
```console
['red', 'blue']
```

With a string:
```python
alphabets = "abcdefghijklmnopqrstuvwxyz"
print(alphabets[::2])
```

Output:
```console
acegikmoqsuwy
```
