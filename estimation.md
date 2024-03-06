# Estimation in system design interviews

By estimation, we mean estimating the needs of the system. This can be the number of servers, the amount of storage, the amount of bandwidth, etc.

Example: Imagine you have a system where low latency matters a lot and you decide to cache the APIs data in memory. You need to estimate how much memory you need to cache the data.

You'll have to learn about the units.

1000 bytes is a kilobyte (KB).

1000 KB is a megabyte (MB).

1000 MB is a gigabyte (GB).

1000 GB is a terabyte (TB).

1000 TB is a petabyte (PB).

General values good to have in mind:

- A character -> 1 byte
- Typical metadata excluding images 1 - 10 kb
- A high quality image -> 2 MB, can be compressed by 10-20x
- 20 minutes of hd video -> 1gb

- Storage: 10TB disk space
- 256gb-1tb of ram

- How long does it take for a regylar http request to make a round trip, not bound by bandwidth?
- Within a country 50ms - 150ms
- Across continents 200ms - 500ms

- Bandwidth cheat sheet
