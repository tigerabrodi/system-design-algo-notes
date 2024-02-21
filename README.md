# Design Fundamentals

Four categories:

- Foundational knowledge: Basic concepts to even begin tackling a design.
- Key characteristics: Latency, throughput, consistency, availability, partition tolerance.
- Actual components: Load balancers, databases, caches, proxies, etc.
- Actual Technologies: Redis, S3, Memcached, Cassandra, etc.

# Client-Server Model

Clients sends requests to servers, servers process requests and send back responses.

Let's take an example, a web browser and the Youtube server.

At first, client knows nothing about the server. That's where DNS comes in. It resolves the domain name to an IP address.

IP address is a unique identifier for the server. It's like a phone number. In the world of internet, communication happens through IP addresses.

Once the client knows the IP address, it can send an HTTP request to the server.

HTTP stands for HyperText Transfer Protocol. It's a protocol that defines how the client and server should communicate.

When you make a request to a server, you don't just have to specify the IP address, you also have to specify the port number. Port number is like an extension number. It's a way to specify which service you want to talk to on the server.

It's because every server can run multiple services. For example, a web server can also run an email server. So, you have to specify which service you want to talk to.

# Network Protocols

A protocol is just a set of rules that define how two entities should communicate.

## IP

IP stands for Internet Protocol. It's a protocol that defines how data should be sent across the internet.

Modern internet runs on IP. Machines communicate with each other using IP. They send IP packets to each other.

There are multiple versions of IP, main ones are 4 and 6. IPv4 and IPv6.

An IP packet is a small chunk of data. IP packet contains:

- header: metadata about the packet e.g. source, destination, total size, version of IP. Between 20 and 60 bytes.
- rest of the part is the actual data. Maximum size is 2^16 bytes. It's a problem because it's too small for modern applications. That's why we need to send multiple packets to send a single file.

## TCP

This is where protocols like TCP come in.

TCP stands for Transmission Control Protocol. It's a protocol that defines how to send data across the internet. It solves the problem of IP packets being too small. It allows us to send large files across the internet and ensures that the data is delivered in the correct order.

In the data part of the IP packet, we have a TCP header and the actual data. TCP header contains metadata about the data e.g. source port, destination port, sequence number, acknowledgment number, etc.

TCP handshake: Before sending data, the client and server have to establish a connection. This is done through a three-way handshake:

1. Client sends a SYN packet to the server. SYN stands for synchronize. It's a request to establish a connection.
2. Server sends a SYN-ACK packet to the client. It's a response to the client's request. It acknowledges the client's request and also sends a request to establish a connection.
3. Client sends an ACK packet to the server. It acknowledges the server's request.

We need HTTP however, because TCP is just a protocol for sending data. It doesn't define how the data should be structured. That's where HTTP comes in.

## HTTP

HTTP stands for HyperText Transfer Protocol. It's a protocol that defines how the client and server should communicate.

It's needed on top of TCP because TCP is just a protocol for sending data. It doesn't define how the data should be structured.

Requests typically look like this:

```
host: www.youtube.com
port: 80
method: GET
path: /watch?v=123
headers: pair list
body: sequence of bytes
```

Responses typically look like this:

```
status code: 200
headers: pair list
body: sequence of bytes
```

# Storage

A database is just a server. It's a server that stores data. Your computer itself can be a database server.

If a power outage happen and database is back, will data be there? Well, not always, and it is an incorrect assumption to think that it will be there.

This leads to two fundamental concepts in databases:

- Disk
- Memory

Writing data to disk guarantees that the data will be there even if the power goes out. But writing to disk is slow. Reading from disk is also slow.

Writing to memory is fast. Reading from memory is also fast. But memory is volatile. If the power goes out, the data is lost.

# Latency and Throughput

## Latency

How long it takes for data to travel from one point to another e.g. how long it takes for a request to travel from the client to the server.

Reading 1MB sequentially from memory takes about 250 microseconds. Reading 1MB sequentially from SSD takes about 1 millisecond which is 4 times slower than memory aka 1000 microseconds.

1 MB over 1 Gbps link takes about 10 000 microseconds.

Packet round trip time from California to Netherlands and back takes about 150 milliseconds aka 150 000 microseconds.

Video games would want to have low latency. They want to have a fast response time. Lag in games is a result of high latency.

## Throughput

How much data can be transferred from one point to another in a given amount of time e.g. how many requests can be processed per second.

This is measured in bits per second. 1 Gbps link can transfer 1 billion bits per second.
