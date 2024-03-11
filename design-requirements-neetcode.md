# Design Requirements

At the fundamental level of a system, we are:

1. Moving data: Moving data from one place to another, whether it's from a user to a server, from a server to a database, or from a database to a user.
2. Storing data: Storing data in a way that makes it easy to retrieve and use, e.g. using database, blob storage, etc.
3. Transforming Data: Transforming data to something more useful e.g. transforming raw data into a graph, or transforming a graph into a list.

## What's a good design?

We have to think in terms of trade offs, but even then, how do we know what's a good design?

How do we measure the trade offs?

### Availability

One way to do so is to measure availability of the system.

Availability is the probability that a system is operational at a given point in time.

For example, if our system was up 23 hours of 24 hours, every day, this would mean our system is up 96% of the time. 100% availability is not possible, e.g. a disaster could happen.

If your system is available for 99% of the time, it means you have a downtime of 1%. Improving your availability to 99.99% would mean you have a downtime of 0.01%, this is a very good improvement, even though it looks small, don't let it fool you.

Availability is measured in nines, e.g. 99.9% is three nines, 99.99% is four nines, etc. These nines are yearly, so 99.9% availability means your system is down for 8.76 hours a year. 99.999%, 5 nines, means your system is down for 5.26 minutes a year.

### SLO

Availability is an SLO, a Service Level Objective. It's a target that you set for your system. It's a promise you make to your users.

SLOs are important because they help you measure how well your system is doing. They help you measure how well you are meeting your users' expectations.

SLOs are a part of SLAs, Service Level Agreements. SLAs are contracts between you and your users. They define what your users can expect from your system.

e.g. AWS S3 has an SLA of 99.99% availability. This means that AWS promises that S3 will be available 99.99% of the time. If it's not, AWS will give you a partial refund.

SLA is not a goal, it's an agreement. SLO is a goal.

## Reliability

Reliability is the ability of a system to perform its functions under normal conditions. It's the probability that a system will work as expected.

Reliability is closely related to availability. If a system is reliable, it's available. But if a system is available, it doesn't mean it's reliable.

For example, a system may be available, meaning it is up and running, but it may not be reliable, meaning it's not performing as expected.

If you've a single server, a way to increase reliability is to add more servers. This is called redundancy. If a server goes down, the system can still work, because the other servers are still running.

## Throughput

Throughput is the number of requests a system can handle in a given amount of time. For example, if a system can handle 1000 requests per second, its throughput is 1000 requests per second.

You can measure throughput in requests per second, or in bytes per second, etc.

You can increase throughput by adding more servers.

We could scale the system vertically, but that still has a limit and a single point of failure. We could scale the system horizontally, by adding more servers. This introduces complexity, because we need e.g. a load balancer, but it's a good trade off.

By scaling the system horizontally, we can increase throughput, availability, and reliability.

Throughput is defined by bytes/second or request/second or queries/second also knows as QPS.

## Latency

Latency is the time it takes for a request to be processed. It's the time it takes for a request to go from the client to the server, and for the server to process the request and send a response back to the client.

You can increase latency by e.g. having servers distributed across the world closer to the users.

Edge locations can help reduce latency, those are locations not in the main data center, but closer to the users.
