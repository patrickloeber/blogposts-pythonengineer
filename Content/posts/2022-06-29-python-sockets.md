---
title: Socket Programming in Python
date: 2022-06-29 00:00
description: Learn how to create web socket client and server in Python using socket module
tags: Python, Intermediate
path: python-sockets
author: Pratik Choudhari
---

Web Sockets allow bi-directional between client and server whereas REST APIs do not offer a full-duplex connection. Python has built-in support for creating server sockets and connecting to them as a client.

In this blog, we will understand Python’s `sockets` module with a few examples of how to create a web socket server and connect using a client.

## Understanding web sockets

Web socket is a communication protocol to facilitate bi-directional and full-duplex channels for sharing messages, it works in a client-server system. Unlike HTTP, the connections in web sockets are established once, persisted and need to be closed formally.

Sockets are of multiple types like TCP and UNIX. They also have a separate URL scheme, for a REST API a URL looks like `http://www.python-engineer.com/blogs/create`  whereas for a web socket `ws://www.python-engineer.com/blogs/comments?id=471`

Areas of application for web sockets include real-time updates and push-based events.
Next, we will be looking at how to create a socket server in Python.

## Creating a socket server

The way a socket server works is very different as compared to a REST API server. As socket TCP connections are persistent, each client connection is kept alive until it is explicitly closed.

The following steps are performed on a socket server:
We bind the server to a host and port number
Listen for incoming connections
Accept new connections
While the connection is alive, listen for messages from a client

Web socket server:

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
The verbs bind, listen, accept, send, recv, close are most used in socket programming.
The sockets object is created using `socket()` method, this socket has to be bound to a host and port we achieve this using `bind()`. `listen()` method asks the socket server to look out for pending connection requests, it takes a number as a parameter which defines the number of unaccepted connections allowed before declining an incoming request.

Once a connection request is received it is accepted using the `accept()` method, it is important to note that the server has to run indefinitely to keep listening for new connections and accept them. `accept()` returns two objects, first is a socket connection object and second is the address of the client. Any further communication with a client is performed using this connection object returned by accept. Next, the server waits for a message from the client using the `recv()` method which takes the max number of bytes to receive from the client at a time and returns the data sent by the client as bytes.

As one can see, the server waits for new connections indefinitely without any timeout also as long as a connection is alive, the server can not accept new connections because every connection is blocking. We will improve this server using multi-threading to work with multiple connections simultaneously.

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

Creating a socket client is simple, a client just connects to the server address and sends data as and when needed, once all messages are exchanged the connection is closed.

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



