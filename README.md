# zapHTTPd

`zapHTTPd` implements a small and efficient web server with 1K lines of C code.
I/O multiplexing is achieved using [epoll](http://man7.org/linux/man-pages/man7/epoll.7.html).

## Features

* Single-threaded, non-blocking I/O based on event-driven model
* HTTP persistent connection (HTTP Keep-Alive)
* A timer for executing the handler after having waited the specified time

## High-level Design

```text
+----------------------------------------------+
|                                              |
|  +-----------+   wait   +-----------------+  |  copy   +---------+
|  |           +---------->                 +------------>         |
|  | IO Device |    1     | Kernel's buffer |  |   2     | Process |
|  |           <----------+                 <------------+         |
|  +-----------+          +-----------------+  |         +---------+
|                                              |
+----------------------------------------------+
```

## Build from Source

At the moment, `zapHTTPd` supports Linux based systems with epoll system call.
Building `zapHTTPd` is straightforward.
```shell
$ mkdir -p .git/hooks
$ make
```

### Default server 
```shell
./zaphttpd
```

### Specify the port
```shell
./zaphttpd -p 8082 
```

Specify the port number with `-p` flag, by default the server accepts connections on port 8081.

### Specify the web root
```shell
./zaphttpd -w ./www
```

Specify the web root with `-w` flag, by default the web root is "./www".

## License
`zapHTTPd` is released under the MIT License. Use of this source code is governed
by a MIT License that can be found in the LICENSE file.
