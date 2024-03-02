# Rate Limiting

Rate limiting is a technique that limits the number of requests that can be made to a server in a given time period. It's a way to prevent abuse and ensure that the server can handle a large number of requests.

For example, if you have a client, server and database, you may want to limit the number of requests that the client can make to the server in a given time period. This is to prevent the server from being overwhelmed by too many requests.

For example, you may accept 100 requests per second from a single client. If the client exceeds this limit, you may want to return an error message to the client. The error status code `429 Too Many Requests` is often used for this purpose.

Rate limiting a server protects it from e.g. DoS (Denial of Service) attacks, where an attacker tries to overwhelm the server with too many requests. They do this in order to make the server unavailable to other users. From bad actors to bugs, rate limiting can help protect your server from being overwhelmed.

You can rate limit based on different things, region, IP Address, user, etc. You can also rate limit based on different time periods, such as per second, per minute, per hour, etc.

Rate limiting isn't the ultimate way of protecting your server, but it's a good start. It's a way to prevent abuse and ensure that the server can handle a large number of requests.

For example, DDoS (Distributed Denial of Service) attacks are a type of DoS attack where an attacker uses multiple machines to overwhelm a server. Rate limiting can help protect your server from DoS attacks, but DDoS attacks are more difficult to protect against, here you will need more advanced techniques such as load balancing, firewalls, etc.
