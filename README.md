# Multi-Threaded Proxy Server with and without Cache

This project is implemented in **C** and demonstrates a **multi-threaded proxy server** that operates with or without caching functionality. The project utilizes threading mechanisms like **semaphores** for handling concurrency and implements a caching mechanism using the **LRU (Least Recently Used)** algorithm.

> HTTP parsing was referred from [this Proxy Server](https://github.com/vaibhavnaagar/proxy-server).

---

## Table of Contents

- [Project Overview](#project-overview)
- [Features](#features)
- [Motivation and Benefits](#motivation-and-benefits)
- [Implementation Details](#implementation-details)
  - [Multithreading](#multithreading)
  - [Cache Mechanism](#cache-mechanism)
- [How to Run](#how-to-run)
- [Demo](#demo)
- [Limitations](#limitations)
- [Possible Extensions](#possible-extensions)
- [Contributing](#contributing)
- [License](#license)

---

## Project Overview

The **Multi-Threaded Proxy Server** intercepts HTTP requests from clients, forwards them to the destination server, retrieves the response, and serves it back to the client. The server has two main modes of operation:
- **With Cache**: The proxy caches the content using the **LRU algorithm** to optimize future requests.
- **Without Cache**: The proxy simply forwards requests and responses without storing them.

It is a multi-threaded system that efficiently handles multiple simultaneous requests, ensuring high performance and low latency.

---

## Features

- **Multi-threaded proxy server** to handle multiple client requests concurrently.
- **Semaphore-based synchronization** for safe multithreading without race conditions.
- **Cache**: Implemented using the **Least Recently Used (LRU)** algorithm for efficient caching of responses.
- Supports **HTTP GET requests**.
- **Concurrency handling** using semaphores to manage shared resources between threads.
- Easy to switch between caching and non-caching modes.
  
---

## Motivation and Benefits

This project serves multiple purposes, including:
- Understanding how a proxy server handles **HTTP requests** and forwards them to servers.
- Managing **multiple client requests** simultaneously and learning about thread synchronization.
- Implementing a **cache** to optimize response times and reduce server load.
- Learning how to use **semaphores** for locking and ensuring thread-safe operations.
- Gaining insight into practical use cases of proxy servers, including improving **network performance**, **restricting access**, and **anonymizing traffic**.

---

## Implementation Details

### Multithreading

- The proxy server uses **semaphores** instead of condition variables or `pthread_join()` to handle concurrency.
- **`pthread_join()`** requires a thread ID for synchronization, whereas **`sem_wait()`** and **`sem_post()`** do not, simplifying thread management.
- Each client request is handled in a separate thread, allowing the proxy to serve multiple clients simultaneously.

### Cache Mechanism

- The caching mechanism uses the **Least Recently Used (LRU)** algorithm to store and retrieve HTTP responses.
- Cache entries are stored in a linked list, where the least recently accessed items are removed when new content needs to be cached.
- This helps to reduce **server traffic** and speed up responses for frequently accessed resources.
  
---

## How to Run

To run the proxy server on your local machine, follow these steps:

1. **Clone the repository**:
    ```bash
    git clone https://github.com/Lovepreet-Singh-LPSK/MultiThreadedProxyServerClient.git
    ```

2. **Navigate to the project directory**:
    ```bash
    cd MultiThreadedProxyServerClient
    ```

3. **Compile the project**:
    ```bash
    make all
    ```

4. **Run the proxy server**:
    ```bash
    ./proxy <port_number>
    ```

    Example:
    ```bash
    ./proxy 8080
    ```

5. **Access the proxy** via a web browser or terminal:
    Open your browser and enter:
    ```
    http://localhost:<port_number>/https://www.example.com
    ```

    Example:
    ```
    http://localhost:8080/https://www.cs.princeton.edu/
    ```

### Note:
- This code can only be run on a **Linux machine**.
- Make sure to **disable your browser's cache** when testing.
- To run the proxy **without cache**, rename the file from `proxy_server_with_cache.c` to `proxy_server_without_cache.c` in the Makefile.

---

## Demo

Here’s how the caching mechanism works:

![](https://github.com/Lovepreet-Singh-LPSK/MultiThreadedProxyServerClient/blob/main/pics/cache.png)

- **Cache Miss**: When a website is accessed for the first time (`URL not found`), the proxy fetches it from the original server and caches it.
- **Cache Hit**: If the website is requested again, the proxy retrieves the response from the cache, which speeds up the process.

---

## Limitations

- **Handling Multi-Client URLs**: If a URL opens multiple clients (such as media content), the cache will store each client's response separately, leading to partial responses.
- **Fixed Cache Size**: Large websites may not fit in the cache due to a fixed element size, limiting the effectiveness of caching for large responses.

---

## Possible Extensions

This project can be extended in several ways:
- **Multiprocessing**: Improve performance further by using multiprocessing, which can utilize multi-core systems for parallelism.
- **Advanced Filtering**: Implement a rule-based system to filter and allow/block certain types of websites.
- **Extended HTTP Support**: Add support for HTTP requests like **POST**, along with additional HTTP methods.
- **Security Features**: Implement features like **request encryption** to protect client data from unauthorized access.

---

## Contributing

We welcome contributions! If you have ideas or improvements, feel free to contribute by following these steps:

1. Fork the repository.
2. Create a new branch (`git checkout -b feature-branch`).
3. Commit your changes (`git commit -m 'Add new feature'`).
4. Push the changes (`git push origin feature-branch`).
5. Open a pull request and submit your changes for review.

Pull requests and suggestions for extending the project are highly appreciated!

---

## License

This project is licensed under the **MIT License**. You can find more details in the `LICENSE` file.

---

## Enjoy Coding!
