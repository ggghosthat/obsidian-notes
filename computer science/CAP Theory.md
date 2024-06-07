In theoretical computer science the CAP theorem (also named Brewer's theorem) states thats any distributed data store con provide only two of the following three guarantees:

- ==Consistency (C)==
	All clients see the some data at the same time, no matter which node they connect to. (Every read receives the most recent write or an error).
- ==Availability (A)==
	 Availability means that any client making a request for data gets a response, even if one or more nodes are down. Another way to state this—all working nodes in the distributed system return a valid response for any request, without exception. Every request receives a (non-error) response, without the guarantee that it contains the most recent write.
- ==Partition tolerance (P)==
	 A partition is a communications break within a distributed system—a lost or temporarily delayed connection between two nodes. Partition tolerance means that the cluster must continue to work despite any number of communication breakdowns between nodes in the system.

NoSQL databases are classified based on the two **CAP** characteristics they support:
- **CP database**: delivers **consistency** and **partition tolerance** at the expense of availability. When a partition occurs between two nodes, the system has to shut-down the non-consistent node (make it unavailable) until the partition is resolved.
- **AP database**: delivers **availability** and **partition-tolerance** at the expense of consistency. When a partition occurs, all nodes remain available but those at the wrong end of partition might return an older version of data than others.
- **CA database**: delivers **consistency** and **availability** across all nodes. It can't do this if there is a partition between any two nodes in the system, however, and therefore can't deliver fault tolerance.
We listed the CA database type last for a reason—in a distributed system, partitions can’t be avoided. So, while we can discuss a CA distributed database in theory, for all practical purposes a CA distributed database can’t exist. This doesn’t mean you can’t have a CA database for your distributed application if you need one. Many relational databases, such as PostgreSQL, deliver consistency and availability and can be deployed to multiple nodes using replication. However this solution will rapidly increase resource consumption. (RAM, another hardware, etc)