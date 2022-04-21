---
title: How to use ThreadPoolExecutor in Python
date: 2022-04-21 00:00
description: Optimize your code using thread pools
tags: Python, Basics
path: threadpoolexecutor
author: Pratik Choudhari
---

If a Python program is heavy on the I/O side, running it in a sequential/synchronous pattern can take a lot of time, and the execution time here can be reduced many folds using threading.

In this article, we are going to talk about Python's `ThreadPoolExecutor` to execute function instances in threads.

## About ThreadPoolExecutor

A normal Python program runs as a single process and a single thread but sometimes using multiple threads can bring lots of performance improvements. 
Creating new threads and managing them can be daunting, thankfully there are a few solutions available.

The `concurrent` Python module is a part of the standard library collection.
`ThreadPoolExecutor` provides an interface that abstracts thread management from users and provides a simple API to use a pool of worker threads. It can create threads as and when needed and assign tasks to them.

In I/O bound tasks like web scraping while an HTTP request is waiting for the response another thread can be spawned to continue scraping other URLs. 

## Using ThreadPoolExecutor

### Submitting multiple tasks

Take the following example:

```python
from concurrent.futures import ThreadPoolExecutor

pool = ThreadPoolExecutor(max_workers=8)

for task in pool.map(my_task, arguments):
    print(task)
```

First, create an instance of `ThreadPoolExecutor`. Next, we have to declare the number of worker threads, a rule of thumb is to use the number of cores in a CPU plus 4

Total Threads = No. of cores + 4

The `map()` method is used to assign tasks to worker threads, this action is non-blocking. 
It returns a generator object, which on iteration returns the output of the target function, blocking the interpreter process.

### Submitting a single task

```python
from concurrent.futures import ThreadPoolExecutor

pool = ThreadPoolExecutor(max_workers=8)

task = pool.submit(my_task, argument)
print(task.result())
```
The `submit()` method is used to submit a task in the thread pool, this action is non-blocking. To get the actual result use the result() method, as the function is executed this method is blocking.
