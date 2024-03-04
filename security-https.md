# Security and HTTPS

## HTTP

HTTP is a protocol built on top of TCP/IP. It is a stateless protocol, meaning that each command is executed independently, without any knowledge of the commands that came before it. It's nice because it's simple, but it's not secure.

HTTP is not secure. It's vulnerable to man-in-the-middle attacks, where an attacker intercepts the communication between the client and the server. Someone who comes in the middle, even though we expect the communication to be secure and private. This is because HTTP is a stateless protocol, meaning that each command is executed independently, without any knowledge of the commands that came before it. This means that there's no way to verify the identity of the server, and no way to verify the integrity of the data.

How does man in the middle attacks happen? When you send a request to a server, the request is sent in plain text. This means that anyone who can intercept the request can read it. They can also modify the request, and send it on to the server. The server will then send a response back to the attacker, who can modify the response, and send it on to the client. The client will then receive the modified response, and have no way of knowing that it has been tampered with.

## HTTPS

HTTPS is a secure version of HTTP. It's a combination of HTTP and SSL/TLS (Secure Sockets Layer/Transport Layer Security). It's secure because it encrypts the data that's being sent, and it verifies the identity of the server.

To understand HTTPS, we first have to dive into how encryption works.

The idea behind encryption is to take some data, and scramble it in such a way that only someone who has the key can unscramble it. The key is a piece of information that's used to encrypt and decrypt the data. There are two types of encryption: symmetric and asymmetric.

## Symmetric Encryption

Symmetric encryption is a type of encryption where the same key is used to encrypt and decrypt the data. This means that the key has to be kept secret, because anyone who has the key can decrypt the data. The most common algorithm used for symmetric encryption is the Advanced Encryption Standard (AES).

The drawback of symmetric encryption is that the key has to be shared between the client and the server. This means that the key has to be sent over the network, which is not secure. If an attacker intercepts the key, they can decrypt the data.

Or if the key gets compromised, the attacker can decrypt all the data that was encrypted with that key.

## Asymmetric Encryption

Asymmetric encryption is a type of encryption where two keys are used: a public key and a private key. The public key is used to encrypt the data, and the private key is used to decrypt the data. This means that the public key can be shared with anyone, and the private key is kept secret.

e.g. If Alice wants to send a message to Bob, she can use Bob's public key to encrypt the message. Bob can then use his private key to decrypt the message.

If a client wants to send a message to a server, it can use the server's public key to encrypt the message. The server can then use its private key to decrypt the message.

When the server sends a response back to the client, it can use the client's public key to encrypt the response. The client can then use its private key to decrypt the response.

This is nice because the public key can be shared with anyone, and the private key is kept secret. This means that the public key can be sent over the network, and it's not a security risk.

The downside of asymmetric encryption is that it's slower than symmetric encryption. This is because the keys are longer, and the algorithms are more complex. This means that asymmetric encryption is not suitable for large amounts of data.

## SSL/TLS

SSL is a protocol that was developed by Netscape in the 1990s. It's a way to secure the communication between the client and the server. It's based on the idea of using asymmetric encryption to establish a secure connection, and then using symmetric encryption to send the data.

SSL is good because it verifies the identity of the server, and it encrypts the data that's being sent. This means that it's secure against man-in-the-middle attacks.

SSL Flow:

1. The client sends a request to the server, asking for a secure connection.
2. The server sends its public key to the client.
3. The client verifies the server's identity, and then generates a symmetric key.
4. The client encrypts the symmetric key with the server's public key, and sends it to the server.
5. The server decrypts the symmetric key with its private key.
6. The client and the server now have a shared symmetric key, which they can use to encrypt and decrypt the data.
7. The client and the server can now communicate securely.
8. The server sends a response back to the client, and the data is encrypted with the shared symmetric key.

The problem with SSL is that it has security vulnerabilities. This means that it's not secure against modern attacks. This is why SSL has been deprecated, and it's no longer considered secure.

TLS was built on top of SSL, because SSL had drawbacks like security vulnerabilities. TLS is the newer and more secure version of SSL.

## TLS Flow

1. The client sends a request to the server, asking for a secure connection.
2. The server sends its public key to the client.
3. The client verifies the server's identity, and then generates a symmetric key.
4. The client encrypts the symmetric key with the server's public key, and sends it to the server.
5. The server decrypts the symmetric key with its private key.
6. The client and the server now have a shared symmetric key, which they can use to encrypt and decrypt the data.
7. The client and the server can now communicate securely.
8. The server sends a response back to the client, and the data is encrypted with the shared symmetric key.

HTTPS is HTTP over TLS, which means that the data is encrypted and the server is verified.

## TLS Handshake

1. The client sends a request to the server, asking for a secure connection.
2. The server sends its public key to the client.
3. The client verifies the server's identity, and then generates a symmetric key. Symmetric key is a random number that's generated by the client. It's used to encrypt and decrypt the data.
4. The client encrypts the symmetric key with the server's public key, and sends it to the server.
5. The server decrypts the symmetric key with its private key.
6. The client and the server now have a shared symmetric key, which they can use to encrypt and decrypt the data.
