# Akka cluster
# Questions
1. What is akka cluster?
2. What is gossip?
3. Akka Cluster Singleton for what purposes do we use it?
4. Akka Cluster states?
5. Describe a process to mark node unreachable in a cluster.
6. Akka cluster sharding?
7. Gossip and CAP theorem what are we losing?
# Answers
1. Akka Cluster is a module of Akka, a toolkit for building highly concurrent, distributed, and resilient message-driven applications. Akka Cluster provides a fault-tolerant decentralized peer-to-peer based cluster membership service with no single point of failure or single point of bottleneck. It does this using gossip protocols and an automatic failure detector.

2. Gossip is a protocol used in distributed systems for nodes to share information about each other in a decentralized manner. In the context of Akka Cluster, gossip is used to share state about the cluster, such as which nodes are members of the cluster and what their statuses are.

3. Akka Cluster Singleton is used for scenarios where you need to ensure that an actor of a certain type runs on only one node in the cluster at a time. This can be useful for operations that must be performed by a single entity in a distributed system, such as database migrations or coordinating a distributed task.

4. Akka Cluster states represent the lifecycle of a node in the cluster. The states are: Joining, Up, Leaving, Exiting, Down, and Removed. A node starts as Joining when it wants to join the cluster, then moves to Up when it's a fully functional member. When a node is ready to leave the cluster, it moves to Leaving, then Exiting, and finally Removed.

5. In Akka Cluster, a node is marked as unreachable when it fails to respond to a certain number of heartbeat messages. The failure detector in each node monitors the heartbeats of all other nodes and marks them as unreachable if they don't respond in time. Once a node is marked as unreachable, it's up to the downing provider to decide when and how to mark the node as down.

6. Akka Cluster Sharding is a module that provides a way to evenly distribute a large number of actors across the nodes in the cluster. It's useful when you have a large number of persistent actors that need to be distributed and need to be interacted with using their unique identifier.

7. Gossip and CAP theorem: The CAP theorem states that a distributed system can only guarantee two out of three properties: Consistency, Availability, and Partition tolerance. In the context of Akka Cluster, which uses a gossip protocol for sharing state, the system opts for Availability and Partition tolerance. This means that in the event of a network partition, the system might provide an outdated view of the cluster state (i.e., lack strong Consistency) until the partition is resolved.