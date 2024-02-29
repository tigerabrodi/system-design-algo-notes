# Replication and Sharding

## Replication

Imagine you've one database. What do you do if the database goes down? You're out of luck. You can't access your data. You can't write new data. You can't read existing data. You're stuck.

That's where replication comes in. Replication is the process of copying data from one database to another. The goal of replication is to increase the availability of your data. If one database goes down, you can still access your data from another database.

Another benefit of replication is having the database in different locations. This can help with latency. If you have a database in the US and another in Europe, users in Europe can access the European database, and users in the US can access the US database. This can reduce the latency for users in Europe.

Replication helps you achieve:

- **High availability**: If one database goes down, you can still access your data from another database.
- **Disaster recovery**: If one data center goes down, you can still access your data from another data center.
- **Latency reduction**: If you have a database in the US and another in Europe, users in Europe can access the European database, and users in the US can access the US database. This can reduce the latency for users in Europe.

## Sharding

Okay, that's replication, huh, we're saved?

Well, what if our database has grown so large that it doesn't fit on a single machine? What if we have so much data that we need to spread it across multiple machines?

This is where sharding comes in. Sharding is the process of splitting up a large database into smaller, more manageable pieces called shards. Each shard is stored on a separate machine.

Sharding is often used in combination with replication. You can shard your data across multiple machines, and then replicate each shard to increase the availability of your data.

There are multiple different strategies for sharding your data, an example is e.g. users with ID 1-1000 go to shard 1, users with ID 1001-2000 go to shard 2, and so on.

### Hotspot

You've to be careful with the sharding strategy you choose. If you shard your data in a way that causes a hotspot, you can end up with a performance bottleneck. A hotspot is a shard that receives a disproportionate amount of traffic. For example, if you shard your data by user ID, and one user has a disproportionate amount of traffic, you can end up with a hotspot.
