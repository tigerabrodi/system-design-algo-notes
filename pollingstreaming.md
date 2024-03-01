# Polling and Streaming

What if we have to build a system where our clients need the updated data frequently, e.g. monitoring temperature, stock prices, etc.?

We're dealing with data clients need to see regularly updated.

This is where both polling and streaming comes in.

## Polling

Polling is when the client asks the server for data at regular intervals. For example, the client can ask the server for data every 5 seconds.

Polling is good for when the data doesn't change often. For example, if the data changes every 5 minutes, then polling every 5 seconds is a waste of resources.

If you're building a real time app like a chat app, polling may not be the best thing to do. This is because the data changes frequently, and polling every second would be a waste of resources. It's gonna be a trade off where its much load on the server.

This is where streaming comes in.

## Streaming

You can have your client open a long lived connection to the server. This way, the server can send the data to the client as soon as it's available. This is typically done using websockets. You can imagine it like a portal from the server to the client. The server can send the data to the client as soon as it's available.

Servers proactively sending data to clients is often referred to as "push" or "server push".
