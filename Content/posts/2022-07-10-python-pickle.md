---
title: Serialize Python objects using Pickle
date: 2022-07-10 00:00
description: Learn how to save your complex python objects on disk using built-in pickle module.
tags: Python, Basic
path: python-pickle
author: Pratik Choudhari
---

The ability to save complex programming data structures onto disk is one of the major advantages of using Python. 
The process is called Serialization and in this article we are going to take a deep dive into Python's [`Pickle`](https://docs.python.org/3/library/pickle.html) module included in standard libraries.

## What is object serialization?

Object serialization is a technique through which a programming language can convert its data structures into a format which can be persisted on disk and sent via a network.
The process of convert the objects into bytes is often referred to as Marshalling or Pickling, the latter term is used when `pickle` module is used to perform the task.
A well defined serialization protocol not only successfully converts objects into bytes but can also deconstruct these bytes back into language specific constructs.
Modules such as marshall, pickle, dill and joblib are a few libraries in Python that can serialize data.

## The `Pickle` module

The `Pickle` module serializes objects in a Python specific manner, which means unlike JSON which is compatible with multiple languages and technologies pickled objects can only we worked on in Python.
Apart from common data structures like dictionary, tuple, list and set, users can serialize third party data structures like a pandas dataframe, numpy arrays.

### Pickling protocols

There six protocols used by `Pickle` for the data conversion, tha latest protocol is 5 introduced in Python 3.8. 
Every new version of a protocol brought new types of objects which can be serialized and improved conversion speed.

- Protocol version 0 is the original “human-readable” protocol and is backwards compatible with earlier versions of Python.
- Protocol version 1 is an old binary format which is also compatible with earlier versions of Python.
- Protocol version 2 was introduced in Python 2.3. It provides much more efficient pickling of new-style classes.
- Protocol version 3 was added in Python 3.0. It has explicit support for bytes objects and cannot be unpickled by Python 2.x. This was the default protocol in Python 3.0–3.7.
- Protocol version 4 was added in Python 3.4. It adds support for very large objects, pickling more kinds of objects, and some data format optimizations. It is the default protocol starting with Python 3.8.
- Protocol version 5 was added in Python 3.8. It adds support for out-of-band data and speedup for in-band data.

Use `pickle.DEFAULT_PROTOCOL` to get the protocol used by `Pickle` for the python version in use.

### Pickling objects

The module comprises of four methods:

1. `pickle.dump()`
2. `pickle.load()`
3. `pickle.dumps()`
4. `pickle.loads()`

The functions with an s at the end work with strings whereas the other work with file handlers.
We will now understand these functions using code examples.

**1. pickle.dump()**

The arguments accepted are:
1. data: required, object to serialize
2. file: required, file handler
3. protocol: optional, pickle protocol version to use
4. fix_imports: optional, if True pickle tries to map Python2 names to Python3

```python
import pickle
from pandas import DataFrame

obj = {"list": [1, 2], "tuple": (1, 2), "set": {1, 2}, "dict": {1: 3, 2: 4},
        "dataframe": DataFrame({"first name": ["john"], "last name": ["doe"]})}

print(f"Using protocol {pickle.DEFAULT_PROTOCOL} to serialize")
with open("my_pickle.pkl", "wb") as fp:
    pickle.dump(obj, fp)
print("Done")
```

Output on Python 3.6:

```console
Using protocol 3 to serialize
Done
```

This script can run as is, on execution a my_pickle.pkl file will be created in the worling directory.
To create a pickle, a file needs to be opened in write-binary mode as pickle converts data to bytes. 
When a function or class is pickled, the pickled version can not reconstruct the function and class because pickle will store only a reference to the object rather than the contents.

**2. pickle.load()**

This function does deserialization, opposite of what pickle.dump() does. The version of pickle protocol is detected automatically.

The arguments accepted are:
1. file: required, file handler
2. fix_imports: optional, if True pickle tries to map Python2 names to Python3
3. encoding: optional, tell pickle how to decode 8-bit string instances pickled by Python 2

```python
import pickle

with open("my_pickle.pkl", "rb") as fp:
    obj = pickle.load(fp)

for key, value in obj.items():
    print(f"Key={key} Value={value} Type={type(value)}")
```

Output:

```console
Key=list Value=[1, 2] Type=<class 'list'>
Key=tuple Value=(1, 2) Type=<class 'tuple'>
Key=set Value={1, 2} Type=<class 'set'>
Key=dict Value={1: 3, 2: 4} Type=<class 'dict'>
Key=dataframe Value=  first name last name
0       john       doe Type=<class 'pandas.core.frame.DataFrame'>
```

**3. pickle.dumps()**

Where `pickle.dump()` writes data into files, `pickle.dumps()` returns a string representation of pickled information.

The arguments accepted are:
1. data: required, object to serialize
2. protocol: optional, pickle protocol version to use
3. fix_imports: optional, if True pickle tries to map Python2 names to Python3

```python
import pickle
from pandas import DataFrame

obj = {"list": [1, 2]}

print(f"Using protocol {pickle.DEFAULT_PROTOCOL} to serialize")
print(pickle.dumps(obj))
```

Output on Python 3.6:

```console
Using protocol 3 to serialize
b'\x80\x03}q\x00X\x04\x00\x00\x00listq\x01]q\x02(K\x01K\x02es.'
```

**4. pickle.loads()**

The string returned by `pickle.dumps()` is passed as input for `pickle.loads()` and returns a python object reconstructed from the pickle information.

The arguments accepted are:
1. data: required, pickled information as string
2. fix_imports: optional, if True pickle tries to map Python2 names to Python3
3. encoding: optional, tell pickle how to decode 8-bit string instances pickled by Python 2

```python
import pickle

print(pickle.loads(b'\x80\x03}q\x00X\x04\x00\x00\x00listq\x01]q\x02(K\x01K\x02es.'))
```

Output:

```console
{'list': [1, 2]}
```
