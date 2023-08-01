

- In general, pulling an image from a cache is far faster than performing a database read.
- ElastiCache uses shards as a grouping mechanism for individual Redis nodes. So a single node is part of a shard, which in turn is part of a cluster.

- Consider ElastiCache as only useful for storing transient data. Further, it’s not a persistent store; therefore, it’s great for caching data from a message queue or providing very fast ephemeral storage.Ø