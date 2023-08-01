


`Data partitioning`: It is the process of distributing data across a set of servers. It improves the scalability and performance of the system.

`Data replication`: It is the process of making multiple copies of data and storing them on different servers. It improves the availability and durability of the data across the system

!!! tip
    A carefully designed scheme for partitioning and replicating the data enhances the performance, availability, and reliability of the system and also defines how efficiently the system will be scaled and managed.


A naive approach will use a suitable hash function to map the data key to a number. Then, find the server by applying modulo on this number and the total number of servers.

!!! warning
    The scheme described in the above diagram solves the problem of finding a server for storing/retrieving the data. But when we add or remove a server, all our existing mappings will be broken. This is because the total number of servers will be changed, which was used to find the actual server storing the data. So to get things working again, we have to remap all the keys and move our data based on the new server count 😕


