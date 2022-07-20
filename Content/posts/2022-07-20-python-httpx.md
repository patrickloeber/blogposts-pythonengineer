---
title: Getting started with the HTTPX module in Python
date: 2022-07-20 00:00
description: A beginners guide to an async capable request library.
tags: Python, Basic
path: python-httpx
author: Pratik Choudhari
---

[Httpx](https://www.python-httpx.org/) is a module capable of making async requests in Python unlike the built-in urllib or third party requests module which have only sync capablities.
In this article, we will explore how async requests are made using the library.

## Installation

Httpx is supported in Python3.6 and above. Install httpx via pip

```python
pip install httpx
```

Note: Linux users should use pip3 instead of pip

## Sync requests

The sync interface of httpx is same as the requests library except when the response is a stream we will look into this in a section below. 
To get started with the requests library, check out this comprehensive guide.

Example:

```python
import httpx

response = httpx.get("https://hub.dummyapis.com/employee?noofRecords=10&idStarts=1001")
print(response.text)
```

Similarly, calls for other request types can be made.

## Async requests

This is where httpx shines. In total, three async environments are supported namely asyncio, trio and anyio of these asyncio is built-in and other two need to be installed explicitly.
Unlike sync requests, async requests need a `AsyncClient` to be initialized before making any calls, this has added advantages such as HTTP connection pooling, cookie persistence and reduced memory and CPU usage.

```python
import asyncio
import httpx

async def main():
    async with httpx.AsyncClient() as aclient:
        response = await aclient.get("https://hub.dummyapis.com/employee?noofRecords=10&idStarts=1001")
    print(response.text)

asyncio.run(main())
```

As we are using a async client the request call needs to be awaited.
It is recommended to use `AsyncClient` in a context manager, the connection can be closed manually using `aclient.aclose()`.

## Streaming requests

To make a request call the response for which would be a stream, the http verb method can not be used directly instead the `stream()` method is used.

```python
import httpx

data = b''
with httpx.stream("GET", "https://speed.hetzner.de/100MB.bin") as response:
    for chunk in response.iter_bytes():
        data += chunk
print(data)
```

The variable `data` will contain response data as bytes.

Streaming response can be iterated in four ways:
- `response.iter_raw()`: read data raw without decoding
- `response.iter_text()`: read data as text
- `response.iter_bytes()`: read data as bytes
- `response.iter_lines()`: read data as lines of text

Async version of streaming response:

```python
import asyncio
import httpx

async def main():
    data = b''
    async with httpx.AsyncClient() as aclient:
        async with aclient.stream("GET", "https://speed.hetzner.de/100MB.bin") as response:
            async for chunk in response.aiter_bytes():
                data += chunk
    print(data)

asyncio.run(main())
```
