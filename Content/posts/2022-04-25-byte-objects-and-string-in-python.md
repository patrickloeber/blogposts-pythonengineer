---
title: Difference between byte objects and string in Python
date: 2022-05-01 00:00
description: Learn the difference between byte objects and string in Python.
tags: Python, Basics
path: byte-vs-string-objects
author: Shweta Goyal
---

There are times when you get confused between byte objects and strings. But there are some differences between them. Let's discuss the difference between them:

## String

Strings are sequences of characters. They are human-readable. They can't be directly stored on the disk, you have to [encode](https://docs.python.org/3/library/stdtypes.html#str.encode) them into a machine-readable format that is bytes.

- `str.encode(encoding='utf-8', errors='strict')`

The default for errors is 'strict', meaning that encoding errors raise a UnicodeError.

There are different forms of encoding like PNG, MP3, ASCII, UTF-8, etc. which are used to represent images, audio, text, etc. in bytes. The default technique is `UTF-8`. Let's take an example to convert a string into bytes:

```python
s = 'Hello world'

# Encoding the string into bytes
bytes_obj = s.encode('ASCII')
print(bytes_obj)

# Output:
b'Hello world'
```

In the above example, we have converted the string into bytes using the `encode()` method. The `encode()` method takes the encoding type as an argument. Here, `b` represents the string in bytes in ASCII form. The `encode()` method returns the bytes object.

## Byte Objects

Byte objects are immutable sequences of bytes, that is, integers in the range 0 to 255. Bytes can be directly stored on the disk. They are machine-readable, you have to [decode](https://docs.python.org/3/library/stdtypes.html#bytes.decode) them into a human-readable format which is a string. If you want it back to its original form then you have to decode it.

- `bytes.decode(encoding='utf-8', errors='strict')`

Let's take an example to convert bytes into strings:

```python
# Byte Object
bytes_obj = b'Hello world'

# Decoding the bytes into string
s = bytes_obj.decode('ASCII')
print(s)

# Output:
'Hello world'
```

In the above example, we have converted the bytes into strings using the `decode()` method. The `decode()` method takes the encoding type as an argument. Here, `ASCII` represents the string in ASCII form. The `decode()` method returns a string.

The byte-like objects can be used in various operations and should be in binary form like file transfer, socket programming, etc.

## Conclusion

In this article, you have learned the difference between byte objects and strings in Python. We have also covered the `encode()` and `decode()` methods. Encoding and decoding are inverse operations. Before storing the data on a computer, you must first encode it. Before reading the data from a computer, you must first decode it.

