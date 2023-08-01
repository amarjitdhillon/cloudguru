

Consistent Hashing maps data to physical nodes and ensures that only a small set of keys move when servers are added or removed.


Consistent Hashing stores the data managed by a distributed system in a ring. Each node in the ring is assigned a range of data. 



<center>

| Server        | Token | Range Start | Range End |
| :-----------  | :---  | :---        |   :---    |
| Server 1      | 1     | 1           | 25        |   
| Server 2      | 26    | 26           | 50        |   
| Server 3      | 51    | 51          | 75        |   
| Server 4      | 76    | 76           | 100        |   

</center>



<center> <img src="../../images/consistentHashingRing.jpg" width="90%"> </center>

The Consistent Hashing scheme described above works great when a node is added or removed from the ring, as in these cases, since only the next node is affected. For example, when a node is removed, the next node becomes responsible for all of the keys stored on the outgoing node. However, this scheme can result in non-uniform data and load distribution. This problem can be solved with the help of Virtual nodes.

