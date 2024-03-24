# Introduction

Imagine we want to build the chat of Twitch. We want to see the chats of users in real-time. One approach we could take is to make HTTP requests every second to get the latest messages. This approach is not efficient because we are making a lot of requests to the server. HTTP is built on top of TCP, which is a connection-oriented protocol. This means that every time we make a request, we need to establish a connection with the server. TCP establishes a connection by performing a three-way handshake. For real-time applications, this approach is not efficient.

# WebSockets

WebSockets is a protocol that provides a two-way communication channel between a client and a server over a single, long-lived connection. The client first makes an HTTP request to the server, then the server upgrades the connection to a WebSocket connection. The status code `101 Switching Protocols` is used to indicate that the server is switching protocols. Once the connection is established, the client and server can send messages to each other in real-time.
