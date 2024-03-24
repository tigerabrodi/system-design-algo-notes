# API

API stands for Application Programming Interface. It simply is a way to access the functionality of a program or a service. APIs are used to interact with other software, similar to how user interfaces are used to interact with humans.

When we talk about APIs, we often refer to working with external APIs. These are APIs provided by third-party services that allow us to interact with their services programmatically. For example, we can use the Twitter API to post tweets, or the Google Maps API to get directions.

However, APIs can also be "internal". Consider arrays in programming languages like JavaScript. Arrays have methods like `push`, `pop`, `shift`, and `unshift` that allow us to interact with them. These methods are part of the array's API.

APIs are just a way to interact with a "thing". This "thing" can be a service, a library, a framework, or even a programming language itself.

In this post, we'll focus on external APIs. We'll dive into REST, GraphQL and gRPC.

# REST

## Introduction

REST stands for Representational State Transfer. REST is built on top of HTTP. This doesn't mean REST is a new protocol, but rather a set of rules to follow when building APIs. People often use REST and HTTP interchangeably, but they are not the same thing. You've likely worked with REST APIs before, even if you didn't know it.

## Stateless

The main thing about REST is that it's stateless. This means that each request from a client to a server must contain all the information needed to understand the request. The server cannot store any information about the client between requests. This makes REST APIs easy to cache and scale. It becomes easy to cache and scale, because each request is independent of the others.

## Resources

REST APIs are built around resources. A resource is an object or representation of something, which has data associated with it. For example, a user is a resource, and a user's name, email, and address are data associated with that resource.

Take a look at the following example: `GET https://youtube.com/videos`. In this example, `videos` is a resource. The `GET` method is used to retrieve the list of videos. The response will contain a list of videos.

## Example

Let's say for example, the response from Youtube contains 10 videos. What if we want to get 10 new videos?

The stateful approach would be for the server to keep track of the last video we saw, and return the next 10 videos.

The stateless approach would be to include a query parameter in the request, like `GET https://youtube.com/videos?start=10`. `start` is the query parameter that tells the server where to start fetching the videos. You might also want `limit` to decide how many videos you want to fetch and not be limited to 10. This way, the server doesn't need to keep track of the last video we saw. And that's what we want in REST!

## Status Codes

REST APIs use status codes to indicate the result of a request. These are from the HTTP protocol. For example, `200 OK` means the request was successful, `404 Not Found` means the resource was not found, and `500 Internal Server Error` means something went wrong on the server.

## Every endpoint related to some resource

Let's look at the example of Youtube again `GET https://youtube.com/videos`. This endpoint is related to the `videos` resource as mentioned. But you might wonder, why we don't have `/getVideos` instead of `/videos`? This is because REST APIs use nouns instead of verbs. The HTTP methods like `GET`, `POST`, `PUT`, `DELETE` are the verbs. The endpoints are the nouns.

## JSON

By far, the most popular format for data exchange in REST APIs is JSON. JSON is a lightweight data-interchange format that is easy for humans to read and write, and easy for machines to parse and generate. It looks like a JavaScript object, but it's a string.

Example of user data in JSON:

```json
{
  "name": "John Doe",
  "email": "john@doe.com",
  "address": "123 Main St"
}
```

# GraphQL

## Introduction

GraphQL is a query language for APIs and a runtime for executing those queries by using a type system you define for your data. It was developed by Facebook in 2012 and released as an open-source project in 2015.

## The idea

GraphQL is built around the idea of asking for what you need, and getting exactly that. With REST, you might need to make multiple requests to different endpoints to get the data you need. With GraphQL, you can make a single request to get all the data you need.

## Example of REST's problem

Let's say we have a REST API for a blog. For each blog post, we need to make a request to get the post, then another request to get the author, and another request to get the comments. This is inefficient because we are making multiple requests to get the data we need. This is where GraphQL shines.

What if we could make a single request to get the blog post, the author, and the comments? Additionally, what if we could specify exactly what fields we need for each of these resources?

## Only POST requests

It's built on top of HTTP. However, you send a POST request to a single endpoint, usually `/graphql`, and you send a query in the body of the request. The query is a string that describes the data you want to get back.

## Two types of operations

In GraphQL, there are two types of operations: queries and mutations.

Queries are used to read data. For example, you might want to get a list of blog posts.

Mutations are used to write data. For example, you might want to create a new blog post, update a blog post, or delete a blog post.

## Caching

GraphQL is built on top of HTTP POST requests. POST requests are not idempotent, meaning the same request can have different results. This makes caching more difficult.

However, GraphQL has a solution for this. You can use a technique called persisted queries. This is where you send a hash of the query instead of the query itself. The server can then look up the query based on the hash. If the query is not found, it can execute the query and store the result in a cache.

## Schema

In GraphQL, you define a schema that describes the data you can query. It defines the types of data you can query, and the relationships between those types. For example, you might have a `Post` type that has a `title` field and an `author` field. The `author` field is a `User` type that has a `name` field.

# gRPC

## Introduction

gRPC is a high-performance, open-source universal RPC framework. It was developed by Google and released as an open-source project in 2015. gRPC is built on top of HTTP/2, which is a major revision of the HTTP protocol.

## Problem with REST

REST APIs are great for many use cases, but they have some limitations.

One of the limitations is that they are text-based. This means that the data is sent over the network as text, which can be inefficient because text takes up more space than binary data. gRPC solves this problem by using Protocol Buffers.

Another limitation is that REST APIs are synchronous. This means that the client has to wait for the server to respond before it can continue. gRPC solves this problem by using HTTP/2, which allows for bidirectional streaming.

## HTTP/2

HTTP/2 is the second major version of the HTTP protocol. It comes with several improvements over HTTP/1.1, to name a few:

- Multiplexing: allows multiple requests and responses to be sent and received at the same time.
- Header compression: reduces the size of the headers, which reduces the amount of data that needs to be sent over the network.
- Server push: allows the server to send resources to the client before the client requests them.
- Bidirectional streaming: allows the client and server to send a stream of messages to each other at the same time.

It's important to mention HTTP/2 because gRPC needs HTTP/2 to work. The reason gRPC needs HTTP/2 is because it uses bidirectional streaming.

### Web Sockets become unnecessary

With HTTP/2, we can use bidirectional streaming. This means that we can send a stream of messages to the server and receive a stream of messages from the server at the same time. This makes Web Sockets unnecessary.

A "stream" is a sequence of messages. For example, you might have a stream of chat messages, where each message is sent as a separate message in the stream. A stream is different from a request-response, where you can only send one message at a time. With a stream, you can send multiple messages at the same time.

## gRPC-Web

gRPC needs detailed control over the HTTP/2 connection, which is not possible in the browser. This is why you need a proxy server to convert the gRPC-Web requests to gRPC requests. The proxy server is called `Envoy`.

## Protocol Buffers

Protocol Buffers is a method of serializing structured data. It's similar to JSON, but it's more efficient because it's binary. This means it takes up less space on the network. Protocol Buffers is used to define the messages that are sent and received in gRPC.

The messages are defined in a `.proto` file. Here's an example of a `.proto` file:

```proto
syntax = "proto3";

package example;

message User {
  string name = 1;
  string email = 2;
}
```

This defines a `User` message with two fields: `name` and `email`.

If we want to send a `User` message in a gRPC request, we define a service in the `.proto` file. Here's an example of a service:

```proto
service UserService {
  rpc GetUser(UserRequest) returns (UserResponse) {}
}

message UserRequest {
  string id = 1;
}

message UserResponse {
  User user = 1;
}
```

The downside of Protocol Buffers is that it's not human-readable like JSON. However, it's more efficient because it's in binary format.

## Error handling

In REST, we have status codes to indicate the result of a request. In gRPC, we don't status codes. Instead, we have error messages, and based on those error messages, we handle what went wrong.
