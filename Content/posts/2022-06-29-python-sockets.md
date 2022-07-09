---
title: Socket Programming in Python
date: 2022-07-09 00:00
description: Learn how to create a web socket client and server in Python using the socket module.
tags: Python, Intermediate
path: python-sockets
author: Pratik Choudhari
---

Web Sockets allow a bi-directional channels between client and server whereas REST APIs do not offer a full-duplex connection. Python has built-in support for creating server sockets and connecting to them as a client.

In this blog, we will understand Python’s `sockets` module with a few examples of how to create a web socket server and connect using a client.

## Understanding web sockets

Web socket is a communication protocol to facilitate bi-directional and full-duplex channels for sharing messages. It works in a client-server system. Unlike HTTP, the connections in web sockets are established once, persisted, and need to be closed formally.

Sockets are of multiple types like TCP and UNIX. They also have a separate URL scheme. For a REST API a URL looks like `http://www.python-engineer.com/blogs/create` whereas for a web socket it looks like `ws://www.python-engineer.com/blogs/comments?id=471`

Areas of applications for web sockets include real-time updates and push-based events.

Next, we will be looking at how to create a socket server in Python.

## Creating a socket server

The way a socket server works is very different compared to a REST API server. As socket TCP connections are persistent, each client connection is kept alive until it is explicitly closed.

The following steps are performed on a socket server:

- We bind the server to a host and port number
- Listen for incoming connections
- Accept new connections
- While the connection is alive, listen for messages from a client

Example of a web socket server:

```python
import socket

SERVER = socket.gethostbyname(socket.gethostname())
PORT = 9797

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
    s.bind((SERVER, PORT))
    s.listen(5)
    print(f"[INFO] Listening on {SERVER}:{PORT}")

    while True:
        conn, addr = s.accept()
        with conn:
            print(f"[CONNECTION] Connected to {addr}")
                while True:
                    data = conn.recv(1024)
                    if not data:
                        break
            conn.sendall(f"[CONNECTION] Received {data} from {addr}".encode())
        print(f"[CONNECTION] Disconnected from {addr}")
```

The verbs *bind*, *listen*, *accept*, *send*, *recv*, and *close* are most used in socket programming.

The sockets object is created using the `socket()` method. This socket has to be bound to a host and port. We achieve this using `bind()`.

The `listen()` method asks the socket server to look out for pending connection requests. It takes a number as a parameter which defines the number of unaccepted connections allowed before declining an incoming request.

Once a connection request is received it is accepted using the `accept()` method. It is important to note that the server has to run indefinitely to keep listening for new connections and accept them.

`accept()` returns two objects, the first is a socket connection object and the second is the address of the client. Any further communication with a client is performed using this connection object returned by accept.

Next, the server waits for a message from the client using the `recv()` method which takes the max number of bytes to receive from the client at a time and returns the data sent by the client as bytes.

As one can see, the server waits for new connections indefinitely without any timeout also as long as a connection is alive. The server cannot accept new connections because every connection is blocking.

## Simultanous socket connections

We will improve the server from above using multi-threading to work with multiple connections simultaneously:

```python
import socket
import threading

SERVER = socket.gethostbyname(socket.gethostname())
PORT = 9797


def client_thread(conn, addr):
    with conn:
        print(f"[CONNECTION] Connected to {addr}")
        while True:
            data = conn.recv(1024)
            if not data:
                break
            conn.sendall(f"[CONNECTION] Received {data} from {addr}".encode())
    print(f"[CONNECTION] Disconnected from {addr}")

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
    s.bind((SERVER, PORT))
    s.listen(5)
    print(f"[INFO] Listening on {SERVER}:{PORT}")

    while True:
        conn, addr = s.accept()
        print(f"[INFO] Starting thread for connection {addr}")
        thread = threading.Thread(target=client_thread, args=(conn, addr))
        thread.start()
        
```

Now with multi-threading, each client connected to the server is handled in its own thread.

## Creating a socket client

Creating a socket client is simple, a client just connects to the server address and sends data as and when needed. Once all messages are exchanged the connection is closed.

Let's see an example:

```python
import socket
import time

SERVER = "192.168.56.1"
PORT = 9797

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect((SERVER, PORT))
client.send("Hello world!".encode())
time.sleep(4)
client.shutdown(1)
client.close()
```
