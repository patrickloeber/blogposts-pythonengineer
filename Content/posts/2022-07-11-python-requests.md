---
title: A guide to requests module in Python
date: 2022-07-11 00:00
description: An easy way to make REST calls via an easy to use interface library.
tags: Python, Basic
path: python-requests
author: Pratik Choudhari
---

To make REST API calls, Python has the [`urllib`](https://docs.python.org/3/library/urllib.html) standard module but it is has a relatively difficult interface as compared to the third-party [`requests`](https://requests.readthedocs.io/en/latest/) library.
In this article, we will learn how to use `requests` to make different types of REST calls, attach payloads and parse the response.

## Installation

`requests` can be installed via PyPi using the pip package manager. It is recommended to install third-party libraries in virtual environments.

For Linux:

```console
pip3 install requests
```

For Windows:

```console
pip install requests
```

## Making a request

In total six types of HTTP requests are supported by the module, which are:
1. GET
2. POST
3. PUT
4. DELETE
5. HEAD
6. OPTIONS

Lets make a simple get request.

```python
import requests

response = requests.get("https://hub.dummyapis.com/employee?noofRecords=10&idStarts=1001")
print(response.text)
```

That's it! Similarly, to make other types of requests replace the method name by the HTTP verb like `requests.post()`

## Send data via query parameters, body or headers

Every HTTP `requests` method takes three optional parameters:
- data: dict, json data to be passed in request body
- params: dict, json data which will be later added as query parameter in request URL
- headers: dict, set custom headers or override default ones

Example:

```python
import requests

query_params = {"noofRecords": 10, "idStarts": 1001}
headers = {"user-agent": "my-app/0.0.1"}
body = {}

response = requests.get("https://hub.dummyapis.com/employee", params=query_params, headers=headers, data=body)
print(response.text)
```

## Analyzing response

A `requests.Response` object is returned on a successful API call. 
The status code of a response can be checked via `response.status_code` property which is an integer and will be one of the [HTTP response status codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status).

Next, we will see the different ways in which response can be parsed. Particularly, there are 3 methods to retrieve the response data:
- `response.json()`: returns a evaluated version of json data
- `response.text`: returns the response as a string
- `response.content`: returns response data in the form of bytes
- `response.headers`: returns a dictionary of response headers

Example:

```python
import requests
from pprint import pprint

query_params = {"noofRecords": 1, "idStarts": 1}

response = requests.get("https://hub.dummyapis.com/employee", params=query_params)
print("Response status code:", response.status_code)
print("Response as json:")
pprint(response.json())

print("Response as text:")
print(response.text)

print("Response as bytes:")
print(response.content)

print("Response headers:")
print(response.headers)
```

## Authentication

Basic HTTP authentication can be used out-of-the-box with requests. 
This is done by passing the username and password as tuple in the `auth` parameter or by creating an object of `requests.auth.HTTPBasicAuth`.

```python
import requests
from requests.auth import HTTPBasicAuth

basic = HTTPBasicAuth('user', 'pass')
response = requests.get("http://dummy-api.com/records", auth=("user", "pass"))

# OR

response = requests.get("http://dummy-api.com/records", auth=basic)
```
