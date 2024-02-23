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

# Availability

Availability: How much time is the system operational?

If you purchased a membership on a platform, you expect it to be available 24/7. If it's not, you're not getting your money's worth, and the business itself is losing money.

## High Availability

Some systems require stronger availability guarantees. For example, a hospital's database. If the database goes down, the hospital can't access patient records. This can be life-threatening. Another example is a plane's control system. If the control system goes down, the plane can crash.

## Nines

Availability is often measured in nines. For example, 99.9% availability means that the system is operational 99.9% of the time. This means that the system can be down for 8.76 hours per year.

This is called, two nones, three nines, four nines, five nines, etc. Those translate into downtime per year, month, week and per day.

## SLA

Service Level Agreement. It's a contract between a service provider and a customer. It defines the level of service that the customer should expect. SLAs often include availability guarantees. SLAs are made of multiple SLOs.

## SLO

SLO and SLA are often used interchangeably, however, they are different. SLO stands for Service Level Objective. It's a target value for a service level. It's a part of the SLA.

## How to achieve high availability?

One important thing is not having a single point of failure. If a single component goes down, the entire system goes down. For example, if a single server goes down, the entire system goes down. This is a single point of failure.

To counter this, redundancy is used. Redundancy means having multiple components that can do the same thing. For example, having multiple servers that can serve the same data. Though in this case we'd need a load balancer to distribute the load between the servers.

But wait, now the load balancer is a single point of failure? Yes, it is. So, we need to have multiple load balancers.

This type of redundancy is called passive redundancy. It's called passive because the redundant components are not doing anything. They're just sitting there, waiting for the main component to fail.

Active redundancy is when the redundant components are doing something. For example, having multiple servers that can serve the same data and are all serving the data at the same time.

# Caching

Caching is a technique that stores data in memory. It's a way to speed up the response time of a request.

Caching is used to improved latency of a system.

You can do caching at multiple levels. Client, Server, DB, etc.

Example where its useful: Client makes a lot of requests to the server. The server makes a lot of requests to the database. If the server caches the data, it doesn't have to make requests to the database. This speeds up the response time of the server. Or you could cache between client and server.

Static files are often cached. For example, images, CSS, JavaScript, etc. These files don't change often. So, there's no need to request them from the server every time. They can be cached in the client's browser.

At the server level, you can cache the results of a database query. If the same query is made again, the server can just return the cached result. This speeds up the response time of the server.

## write through cache

When you write to the cache, you also write to the database. This ensures that the cache and the database are always in sync.

Pros:

- Data is always in sync.
- If the cache goes down, the data is still in the database.

Cons:

- Writing to the database is slow.
- If the database goes down, the cache is useless.

## Write back cache

When you write to the cache, you don't write to the database. You just write to the cache. The cache is responsible for writing to the database.

Pros:

- Faster than write through cache.
- If the database goes down, the data is still in the cache.

Cons:

- If the cache goes down, the data is lost.

## Consistency

Caching can cause consistency issues. For example, if the server caches the results of a database query, and the database is updated, the cache is now out of date.

You have to ask yourself, how important is consistency? For example, if you're building a social media platform, consistency is not that important. If a user posts a photo and it takes a few seconds for the photo to show up, it's not a big deal. But if you're building a banking system, consistency is very important. If a user transfers money from one account to another, the money should be transferred immediately.

## General rules

- Cache data that doesn't change often.
- Cache data that's accessed often.
- Cache data that's expensive to compute.
- Cache data that's far away.
- Cache data that's large.

## Cache eviction

When the cache is full, and you want to add new data to the cache, you have to remove some data from the cache. This is called cache eviction.

There are multiple ways to do cache eviction. The most common way is LRU (Least Recently Used).

LRU evicts the data that was accessed the least recently. It's called LRU because it evicts the data that was accessed the least recently.

LRU eviction is a simple way to do cache eviction. It's easy to implement and it works well.

# Proxies

A forward proxy is a server that sits between the client and the server. The client sends requests to the proxy, and the proxy forwards the requests to the server. The server sends responses to the proxy, and the proxy forwards the responses to the client. The forard proxy acts on behalf of the client. This is useful for e.g. privacy and security, serving as a way to hide the client's IP address.

A reverse proxy is a server that sits between the client and the server. The client sends requests to the reverse proxy, and the reverse proxy forwards the requests to the server. The server sends responses to the reverse proxy, and the reverse proxy forwards the responses to the client. The reverse proxy acts on behalf of the server. This is useful for e.g. load balancing, caching, security, etc.

Forward proxy -> Acts on behalf of the client.
Reverse proxy -> Acts on behalf of the server.

They serve different roles.

Reverse proxy is often used for load balancing. Load balancing is a technique that distributes the load between multiple servers. This is useful for improving the throughput of a system.

Forward proxy is often used for caching. Caching is a technique that stores data in memory. This is useful for improving the response time of a system. Forward proxy is also famously used for VPNs.
