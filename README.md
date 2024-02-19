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
