Key-Value store: known as Key-value database, or non-relational database
### Design scope
* The size of a key-value pair is < 10k
* Ability to store big data
* High availability
* High scalability
* Automatic scaling
* Tunable consistency
* Low latency

### Single server key-value store
#### Store key-value paris in a hash table
Two optimizations to fit more data in a single server
* Data compression
* Store only frequently used data in memory and the rest on disk

### Distributed key-value store
#### Understand CAP theorem for designning a distribute system
##### CAP theorem
* Consistency
* Availability
* Partition Tolerance
  * A partition indicates a communication break between two nodes.

CAP theorem states that one of the three properties must be sacrificed to support 2 of the 3 properties.
#### Real-world distributed systems
In a distributed system, partitions cannot be avoided, and when it occurs, we must choose between **consistency** and **availability**.

### System components
* Data partition
* Data replication
* Consistency
* Inconsistency resolution
* Handling failures
* System architecture diagram
* Write path
* Read path

#### Data partition
Two chanllenges:
* Distribute data across multiple servers evenly
* Minimize data movement when nodes are added or removed

**Consistent hashing** in Chapter 5 is a great technique to solve them.
* First, servers are placed on a hash ring
* Next, a key is hashed onto the same ring, and it is stored on the first server encountered while moving clockwise direction.

#### Data replication
Choose N servers for replication using the following logic
* after a key is mapped to a position on the hash ring, walk clockwise from that position and choose the first N servers on the ring to store data copied.
* with virtual nodes, the first N nodes may be owned by fewer than N physical servers.
  * To avoid it, only choose unique servers while performing the clockwise walk logic
  
 #### Consistency
 A few definitions
 * N = The number of replicas
 * W = A write quorum of size W. For a write operation to be consisdered as successful, write operation must be acknowledged from W replicas
 * R = A read quorum of size R. For a read operation to be considered as successful, read operation must wait for responses from at least R replicas.

Configuration of W, R and N is a typical tradeoff between **latency** and **consistency**
