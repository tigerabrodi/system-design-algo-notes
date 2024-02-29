# Peer-to-Peer Networking

Imagine you want to deploy and transfer large files to thousands of machines at once. For example, let's say you get videos from a security camera and you want to transfer these videos to thousands of machines.

5GB files on a 40Gbps network would take 1.25 seconds to transfer. However, if you have 1000 machines, then it would take 20 minutes to transfer the file to all machines. This is because the network is the bottleneck.

To recap thorughput: Gbps is gigabits per second, and GB is gigabytes. 1 byte is 8 bits. So 40Gbps is 5GB/s. This means 1000 machines would take 5GB/s \* 1000 = 5TB/s. 5TB is 5000GB. So 5000GB / 5GB/s = 1000s = 20 minutes.

Imagine you want the security camera to send the videos every 5 minutes. If you have 1000 machines, then it would take 1000 \* 5 minutes = 5000 minutes = 83 hours. This is because the network is the bottleneck.

## First step

So as a first step, we know redundancy is a good step. Instead of having a single server, we decide to have multiple servers. This way, if one server goes down, then we can still transfer the file to the other servers. On top of that, we can transfer files concurrently to all servers.

Let's say we add 10 servers, so we have 10 servers. Now the throughput is 5GB/s \* 10 = 50GB/s. This means 1000 machines would take 5TB / 50GB/s = 100s = 1 minute and 40 seconds. This is a huge improvement from 20 minutes.

However, we run into a trouble, it's more complex, we have to replicate files across servers and we still haven't solved the problem of the network being the bottleneck.

## Peer to Peer Networking comes to play

So, let's go back to the beginning. We have one server. The idea behind peer to peer networking is to have the machines that are receiving the file to also send the file to other machines. This way, we can leverage the network of machines to transfer the file.

You recall we had 5 gb files and the network throughput was 40Gbps. This means we can transfer 5GB in 1.25 seconds. If we have 1000 machines, then it would take 5GB / 40Gbps = 1.25s. This is because the network is the bottleneck.

What if we split down the 5GB file into 1000 pieces, and then each machine sends a piece to another machine. This way, we can transfer the file in 1.25s. This is because the network is the bottleneck.

Then each machine can send the its piece to another machine. Every one of the 1000 machines would be talking to another machine. While they're sending their piece, they're also receiving a piece from another machine. This way, we can take advantage of the network.

This means for every second, we are not just sending out a new chunk/piece the 5MB file from the 1000 we broke down into, but the existing machines that have received a piece are also sending out the piece they have received to another machine. This way, we can take advantage of the network.

## How to know which machine to send to?

This get quickly very complicated.

There are two main ways to do this:

1. Centralized: We have a central server that keeps track of which machine has which piece. This way, when a machine wants a piece, it can ask the central server. This is how BitTorrent works. BitTorrent has a central server called a tracker (often what this central server is generally called in peer to peer networking) that keeps track of which machine has which piece. When a machine wants a piece, it can ask the tracker. The tracker then tells the machine which machine has the piece. The machine can then ask the other machine for the piece.

2. Gossip: We can use a gossip protocol. A gossip protocol is a protocol that allows machines to talk to each other. When a machine wants a piece, it can ask another machine. The other machine can then tell the machine which machine has the piece. The machine can then ask the other machine for the piece. This is how the Cassandra database works. Cassandra uses a gossip protocol to allow machines to talk to each other. It's named gossip because it's like how people gossip, like how a rumor spreads.

DHT: Peers often operate by using a distributed hash table (DHT). A DHT is a distributed system that provides a lookup service similar to a hash table. A DHT is a key-value store. The key is the hash of the file, and the value is the machine that has the file. When a machine wants a piece, it can ask the DHT. The DHT then tells the machine which machine has the piece. The machine can then ask the other machine for the piece. This is how the Kademlia DHT works. Kademlia is a DHT that's used in peer to peer networking.
