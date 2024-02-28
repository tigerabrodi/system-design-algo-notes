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

# Load Balancers

Let's say we start with a client and server. Multiple clients now make requests to the server. The server can't handle all the requests. It's overloaded.

We need to scale, vertically or horizontally. Horizonal scaling is adding more servers. Vertical scaling is adding more resources to the server.

If we add more servers (horizontal scaling), we need a way to distribute the load between the servers. This is where load balancers come in.

Load Balancers sit between the client and the server. The client sends requests to the load balancer, and the load balancer looks at all the servers and decides which server to send the request to. The server sends responses to the load balancer, and the load balancer forwards the responses to the client.

You think of load balancers as reverse proxies. They act on behalf of the server. They distribute the load between the servers.

When adding a new server, you configure the load balancer to distribute the load between the new server and the old servers.

Load balancers can distribute the load in multiple ways. For example, round robin, least connections, IP hash, etc.

What happens if the load balancer itself becomes overloaded? You can add more load balancers. You can also use DNS load balancing. This is a technique that distributes the load between multiple load balancers.

# Hashing

Hashing is a technique that maps data to a fixed size. It's a way to convert data into a fixed size.

For example, 4 clients and 4 servers. Load balancer uses hashing to distribute the load between the servers. It hashes the client's IP address and maps it to a server. This lets us take advantage of caching, we'd know which server to go to for a specific client. Each server would have an in memory cache. If the client makes a request to the server, the server would check the cache first. If the data is in the cache, it would return the data. If the data is not in the cache, it would go to the database and store the data in the cache.

If we add a new server, we'd have to rehash and remod the clients to the servers. This is why this approach is a problem. Because if a server goes down or a new server is added, we'd have to remod the clients to the servers. The in memory caches we had in each server would be useless.

This is where algorithms like consistent hashing come in.

## Consistent Hashing

First, we have a circle. The circle represents the hash space. Each server is represented by a point on the circle. Each client would be hashed to a point on the circle. The client would be mapped to the server that's closest to it in the clockwise direction.

So each client would look at the circle and find the server that's closest to it in the clockwise direction. This is the server that the client would be mapped to.

If a server goes down, the clients that were mapped to that server would be remapped to the next server in the clockwise direction.

If a new server is added, the clients that were mapped to the next server in the clockwise direction would be remapped to the new server.

Let's say you wanna even more evenly want to distributed the load between the servers. You can add virtual nodes. Each server would be represented by multiple points on the circle. This would make the circle more evenly distributed. This is good because it would make the load more evenly distributed between the servers.

For example, if you've multiple servers, but Server A is much more powerful than Server B, you can add more virtual nodes for server A. This would give server A more points on the circle, and thus more load.

## Rendezvous Hashing

Rendezvous hashing is different from consistent hashing. In consistent hashing, the client is mapped to the server that's closest to it in the clockwise direction. In rendezvous hashing, the client is mapped to the server that has the highest score.

A server's score is calculated by hashing the server's name and the client's name. The server with the highest score is the server that the client is mapped to.

Every client would calculate the score for every server and choose the server with the highest score.

## When to choose a hashing strategy?

- Consistent hashing: When you want to evenly distribute the load between the servers.
- Rendezvous hashing: When you want to choose the server with the highest score.
- When servers have an in memory cache and you want to take advantage of caching.

# Relational Databases

Relational databases are databases that store data in tables. Each table has rows and columns. Each row is a record. Each column is a field. A record is a collection of fields. A field is a piece of data.

For example:

```
+----+-------+-----+
| id | name  | age |
+----+-------+-----+
| 1  | John  | 25  |
| 2  | Alice | 30  |
| 3  | Bob   | 35  |
+----+-------+-----+
```

Relational Databases are very structured. Each table has a schema. A schema is a set of rules that define the structure of the table. For example, the schema of the table above is:

```
id: integer
name: string
age: integer
```

The schema defines the structure of the table. It defines the data types of the fields. It also defines the relationships between the fields.

For example, when it comes to relationships, you can have a one-to-one relationship, a one-to-many relationship, or a many-to-many relationship.

Relational databses imposes strict rules on the data. For example, you can't have a record in a table that doesn't have a value for a field. You can't have a record in a table that has a value for a field that's not in the schema.

## SQL

SQL stands for Structured Query Language. It's a language that's used to interact with relational databases. It's a language that's used to create, read, update, and delete data in a relational database.

SQL is a declarative language. It means that you tell the database what you want to do, and the database figures out how to do it.

When dealing with relational databases, you can perform powerful SQL queries. For example, you can perform joins, unions, intersections, etc.

## ACID

ACID stands for Atomicity, Consistency, Isolation, Durability. It's a set of properties that guarantee that database transactions are processed reliably.

- Atomicity: A transaction is atomic if it's either completely processed or not processed at all.
- Consistency: A transaction is consistent if it takes the database from one consistent state to another consistent state.
- Isolation: A transaction is isolated if it's processed independently of other transactions.
- Durability: A transaction is durable if its effects are permanent.

If memorizing ACID is hard, a way to think about it is the naive way of thinking. When you say, I'll make transaction from bank account A to bank account B, you expect it to either happen or not happen, you don't care about the underlying logic. Similar to how you expect it to be permanent after it happens.

This naive way of how we've been thinking about DB operations is what ACID is about after all.

## Database Index

What if you have the problem of having to search through a large table? It's slow. This is where database indexes come in.

You can instead for example, turn O of n into O of log n. This is done by creating an index. An index is a data structure that's used to speed up the search of a table.

You can imagine it as a book index. You look up a word in the index, and the index tells you which page the word is on. This is much faster than looking through the entire book.

However, indexes should be used with caution. They can speed up the search of a table, but they can also slow down the write of a table. This is because when you write to a table, you also have to write to the index. Why do you have to write to the index? Because the index has to be updated. For example, if you add a record to a table, you also have to add a record to the index.

So, when is it befitting to add an index?

- When you have a large table and you want to speed up the search of the table.
- When you perform JOIN operations on a table, these are operations that combine records from two tables. For example, if you have a table of employees and a table of departments, and you want to find the employees that work in a specific department, you'd perform a JOIN operation. This is a slow operation. You can speed it up by adding an index to the table. With an index, the database can look up the records in the table much faster.
- When you have a table that's sorted. For example, if you have a table of employees and you want to find the employees that are older than 30, you can speed up the search by adding an index to the table. With an index, the database can look up the records in the table much faster.

## SQL Indexes

How to create a database index in SQL?

```sql
CREATE INDEX index_name ON table_name (column_name);
```

This creates an index on the column_name of the table_name.

Let's look at another example:

```sql
CREATE INDEX name_index ON employees (name);
```

Here, this would help if you're searching for employees by name. If you want to find all the employees that have a name that starts with "A", you can use the following query:

```sql
SELECT * FROM employees WHERE name LIKE 'A%';
```

This would be much faster than searching through the entire table.

What about a JOIN index?

```sql
CREATE INDEX department_index ON employees (department_id);
```

This would help if you're performing JOIN operations on the employees table and the departments table. For example, if you want to find all the employees that work in a specific department, you can use the following query:

```sql
SELECT * FROM employees JOIN departments ON employees.department_id = departments.id WHERE departments.name = 'Engineering';
```

This query tells us that we want to find all the employees that work in the Engineering department. This is a slow operation. You can speed it up by adding an index to the employees table.

## Transactions in SQL

An example of a transaction in SQL:

```sql
BEGIN TRANSACTION;
UPDATE employees SET salary = salary + 1000 WHERE age > 30;
UPDATE employees SET salary = salary + 2000 WHERE age > 40;
COMMIT;
```

In this example, we're updating the salary of employees. We're updating the salary of employees that are older than 30 and 40. This is a transaction. If we don't commit the transaction, the changes won't be permanent.

While the transaction is running, if other changes in the database are made, they won't be visible to the transaction. This is called isolation. It's a property of transactions.

Consistency in this case would be that the changes are consistent. For example, if the transaction fails, the changes are rolled back. If the transaction succeeds, the changes are permanent.

## Strong vs Eventual Consistency

Strong consistency: If a transaction is processed, the changes are immediately visible to other transactions. This is called strong consistency. It's a property of transactions.

Eventual consistency is another consistency model. Unlike strong consistency, eventual consistency doesn't guarantee that the changes are immediately visible to other transactions. It guarantees that the changes are eventually visible to other transactions.
