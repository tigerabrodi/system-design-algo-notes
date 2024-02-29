# Specialized Storage Paradigms

Databases are one type of storage system, but there are many others. Each type of storage system has its own strengths and weaknesses, and is best suited for different types of data and use cases.

## Blob Storage

Blob is an ancroym for Binary Large Object. Blob is arbitrary piece of data, such as a file, an image, or a video. Blob storage is a type of storage system that is optimized for storing and retrieving blobs. It is often used to store large files, such as images, videos, and backups.

A blob doesn't fit into SQL database, because it's not a structured data. It's just a file. So, you can't query a blob like you can query a SQL database. Instead, you can only retrieve the entire blob at once.

Common blob storage systems include Amazon S3, Google Cloud Storage, and Azure Blob Storage.

They're optimized for storing and retrieving large of unsctructured data, and they're often used to store files, images, videos, and backups.

Usually you would access a blog via a key-value interface, where you provide a key and get back the blob associated with that key.

## Time Series Databases

Time series database is a type of database that is optimized for storing and retrieving time series data. Time series data is data that is indexed by time, such as stock prices, sensor readings, and server logs.

Time series databases are used to store and analyze data that is indexed by time. They're often used to store logs, logs, and other time-based data.

Common use cases: Monitoring, IoT, and financial data.

Common time series databases include InfluxDB, Prometheus, and Graphite.

## Graph Databases

Graph database relies at its core on graph structures for semantic queries with nodes, edges, and properties to represent and store data. A graph database is a type of database that is optimized for storing and retrieving graph data. Graph data is data that is represented as a graph, with nodes and edges.

If you're storing data where there are many relationships between different items, a graph database might be a good choice. For example, social networks, recommendation engines, and fraud detection.

Many-to-many relationships are a good fit for graph databases, but only if you need to query the relationships between the items.

If relations are the core of your data, a graph database might be a good choice.

The most popular graph databases are Neo4j, Amazon Neptune, and Azure Cosmos DB.

For example, in Neo4j, you have a special query language called Cypher, which is designed to work with graph data. You can use Cypher to query and manipulate graph data.

## Spatial Databases

Spatial database is a type of database that is optimized for storing and retrieving spatial data. Spatial data is data that is indexed by location, such as maps, GPS coordinates, and geographic information.

If you're making queries e.g. "find all the restaurants within 5 miles of my current location", a spatial database might be a good choice. SQL databases can do this, but spatial databases are optimized for these types of queries. SQl databases may not be a good choice when you have a lot of spatial data.

Quadtree is a common data structure used in spatial databases. It's a tree-like data structure that is used to store and retrieve spatial data. Quadtrees are used to efficiently store and retrieve data that is indexed by location.

How quadtrees work: You start with a single square that represents the entire area. Then you divide the square into four smaller squares. Then you divide each of those squares into four smaller squares, and so on. Each square is called a "node" in the quadtree. Each node can have zero or more children. Each node represents a region of space, and each child represents a smaller region of space.

You keep dividing the squares until each square contains a small number of data points. Then you store the data points in the squares. When you want to find all the data points within a certain region of space, you can use the quadtree to efficiently find the data points that are in that region.

You can find a location in big o log n time, where n is the number of data points in the quadtree. This is because the quadtree works like a binary search tree, but it has four children instead of two.
