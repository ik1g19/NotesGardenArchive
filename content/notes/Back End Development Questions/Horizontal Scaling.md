Horizontal scaling means adding more machines or nodes to a system to improve performance and ability to handle increased load - rather than upgrading the hardware of an existing machine, which is known as vertical scaling

# MongoDB

Horizontal scaling in MongoDB means adding more machines/nodes to the database cluster

Data is distributed across multiple servers
- Distribution of data across multiple servers is often facilitated by a method called "sharding"
- In "sharding", data is partitioned and each partition is plcaed on a separate database server

Benefits:
- Can handle larger amounts of data and traffic
- Provides high availability, sincei if one node fails then the system can continue to operate using the remaining nodes
- The system can grow by adding more machines to the cluster, allows for a more flexible and cost effective scalability approach

MongoDB supports horizontal scaling through sharding

As data grows, new shards (or servers/nodes) can be added to a MongoDB cluster, and the database will distribute the data among these shards

This allows MongoDB to manage vast amounts of data and traffic while providing redundancy and high availability

---

See also [Vertical Scaling](Vertical%20Scaling.md)