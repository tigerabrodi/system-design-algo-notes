# Leader Election

Let's say you've a product that let's users subscribe e.g. Netflix. Then you've a database that stores the user's subscription information.

Imagine you've a third party service such as Stripe, Paypal, etc. that charges the user's credit card every month. However, you don't want to have the third party service directly charge the user's credit card. Instead, you want to have a service that acts as a middleman between your database and the third party service. This middleman service is responsible for charging the user's credit card every month.

Now, if you only have one middleman service, what happens if it goes down? We have to imagine when building distributed systems that servers and nodes can fail. If the middleman service goes down, then no one is charging the user's credit card. This is a problem. So we can introduce redundancy by having multiple middleman services. But then we have to decide which middleman service is responsible for charging the user's credit card, because we don't want to charge the user's credit card multiple times.

So, we're now gonna have a leader. The leader is responsible for charging the user's credit card. If the leader goes down, then we have to elect a new leader. This is called leader election.

Leader election may sound simple, we just pick a new leader when the current leader goes down. But it's not that simple. We have to consider a lot of things such as network partitions, split brain, etc.

The real difficulty is having the followers agree on who the leader is. We have to make sure that the followers agree on who the leader is. This is called consensus.

This is where consensus algorithms come in. Consensus algorithms are algorithms that allow a group of nodes to agree on a value. Leader election is a special case of consensus. Popular consensus algorithms include Paxos, Raft, and Zab.

## Tools for consensus

Now, you won't implement consensus algorithms from scratch. Instead, you'll use libraries that implement consensus algorithms. These libraries are called distributed consensus systems. Examples of distributed consensus systems include ZooKeeper, etcd, and Consul.

## Etcd

Etcd is a distributed key value store that's highly available and strongly consistent. It's used for shared configuration and service discovery. It's written in Go and uses the Raft consensus algorithm.

Strong consistency here means writing and reading from Etcd will always return the latest value. This is important for leader election. If we have multiple middleman services, we want to make sure that the leader is the latest leader.
