---
title: How to use ThreadPoolExecutor in Python
date: 2022-05-02 00:00
description: Optimize your code using thread pools.
tags: Python, Basics
path: threadpoolexecutor
author: Pratik Choudhari
---

If a Python program is heavy on the I/O side, running it in a sequential/synchronous pattern can take a lot of time, and the execution time here can be reduced many folds using threading.

In this article, we are going to talk about Python's `ThreadPoolExecutor` to execute function instances in threads.

## About ThreadPoolExecutor

A normal Python program runs as a single process and a single thread but sometimes using multiple threads can bring lots of performance improvements.

Creating new threads and managing them can be daunting, thankfully there are a few solutions available.

The `concurrent` Python module is a part of the standard library collection. `ThreadPoolExecutor` provides an interface that abstracts thread management from users and provides a simple API to use a pool of worker threads. It can create threads as and when needed and assign tasks to them.

In I/O bound tasks like web scraping, while an HTTP request is waiting for the response, another thread can be spawned to continue scraping other URLs. 

## Submitting multiple tasks with `map()`

- `map(func, *iterables, timeout=None, chunksize=1)`

*func* is executed asynchronously and several calls to *func* may be made concurrently.

Let's look at an example:

```python
from concurrent.futures import ThreadPoolExecutor

urls = ["python-engineer.com",
        "twitter.com",
        "youtube.com"]

def scrape_site(url):
    res = f'{url} was scraped!'
    return res

pool = ThreadPoolExecutor(max_workers=8)

results = pool.map(scrape_site, urls) # does not block

for res in results:
    print(res) # print results as they become available

pool.shutdown()
```

First, create an instance of `ThreadPoolExecutor`. Next, we have to declare the number of worker threads. The default  value of `max_workers` is `min(32, os.cpu_count() + 4)`.

The `map()` method is used to assign tasks to worker threads. This action is non-blocking. It returns an iterable immediately, which on iteration returns the output of the target function, blocking the interpreter process. The results are available in the order that the tasks were submitted.

Finally, call `shutdown()` to signal the executor that it should free any resources that it is using when the currently pending futures are done executing.

The above code outputs the following:

```console
python-engineer.com was scraped!
twitter.com was scraped!
youtube.com was scraped!
```

## Submitting a single task with `submit()`

- `submit(fn, /, *args, **kwargs)`

Schedules the callable, *fn*, to be executed as `fn(*args, **kwargs)` and returns a `Future` object representing the execution of the callable.

Let's look at an example:

```python
from concurrent.futures import ThreadPoolExecutor

pool = ThreadPoolExecutor(max_workers=8)

future = pool.submit(my_task, argument) # does not block

value = future.result() # blocks

print(value)

pool.shutdown()
```

The `submit()` method is used to submit a task in the thread pool. This action is non-blocking. To get the actual result, use the `result()` method. This method is blocking.

## Use ThreadPoolExecutor as context manager

The recommended way to use a ThreadPoolExecuter is as a context manager. This way `shutdown()` will be called automatically when the block has completed.

```python
with ThreadPoolExecutor(max_workers=1) as pool:
    future = pool.submit(pow, 2, 15)
    print(future.result())
```
