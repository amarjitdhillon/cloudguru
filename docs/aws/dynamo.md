


DynamoDB is a simple database that supports key-value and document-based table design. It is fully-managed and provides high performance at scale. Interestingly, its performance improves with scale.


# Features
## Scaling in Dynamo

It works better on large scale due to consistent hashing.
<center> <img src="../images/dynamo_scaling.jpg" width="90%"> </center>

## Schema

The only schema constraint you have when inserting an item in a table is that the item should have a unique primary key. As long as we provide a unique primary key, we can insert whatever data we want to insert.

## Scaling
Push-button scaling: This is just a very fancy term to say you can scale your instance resources using a graphical user interface. To be precise, it means that you can scale the size of an instance(memory, CPU, PIOPS, disk, etc) either up or down, with the click of a button.


## Partitioning and re-partitioning

AS we know that data is horizontally scaled across multiple servers in Dynamo. This means that the data needs to be partitioned. Also, servers are added and removed all the time, which means that they have to be re-partitioned frequently. You don’t have to worry about that this either, since the partitioning and repartitioning processes are managed by AWS without downtime.

!!! warning "Storing large files in Dynamo"
    Although we can save up to 400 KB of data in one item, if we are trying to save larger files in DynamoDB, we will be at a loss in terms of cost. It would be better for us to use `AWS S3` to store the files and have links to the files in our database 😄

!!! tip
    DynamoDb is running on SSD and have minimum of 3 instances.


## Dynamo Data Model

### Items
Items in DynamoDB are similar to the rows in relational databases. An item belongs to a table and can contain multiple attributes. An item in DynamoDB can also be represented as a JSON object (a collection of key-value pairs).


### Attributes
Each individual key-value pair of an item is known as an attribute. An item is built from multiple attributes. We can think of attributes as the properties of the item when we think of the item as a JSON object. Values of attributes can have many scalar and composite data types

## Primary key
Each table in DynamoDB contains a `primary key`. A primary key is a special set of attributes. Its value is unique for every item and is used to identify the item in the database. Under the hood, it is used to partition and store the data in order.

There are two types of primary keys:

- `Partition key`: Here, we have a unique key of scalar type (string, number, boolean), which determines the storage partition the item will go into.

- `Partition key and Sort key`: Here, we have two keys. The partition key determines the partition where the item goes into the storage and the sort key determines the rank of the item in the partition. **Neither of these two keys need to be unique. However, their combination should be unique.**


## Designing No-SQL Schema

NoSQL design requires a different mindset than RDBMS design. For an RDBMS, you can go ahead and create a normalized data model without thinking about access patterns.

In particular, it is important to understand three fundamental properties of your application's access patterns before you begin:

- `Data size`: Knowing how much data will be stored and requested at one time will help determine the most effective way to partition the data.
- `Data shape`: Instead of reshaping data when a query is processed (as an RDBMS system does), a NoSQL database organizes data so that its shape in the database corresponds with what will be queried. ==This is a key factor in increasing speed and scalability.==
- `Data velocity`: DynamoDB scales by increasing the number of physical partitions that are available to process queries, and by efficiently distributing data across those partitions. Knowing in advance what the peak query loads will be might help determine how to partition data to best use I/O capacity.

## No-SQL best practices for NFR's

### Keep related data together
The single most important factor in speeding up response time: keeping related data together in one place. 

!!! tip
    As a general rule, you should maintain as few tables as possible in a DynamoDB application.Exceptions are cases where high-volume time series data are involved, or datasets that have very different access patterns. A single table with inverted indexes can usually enable simple queries to create and retrieve the complex hierarchical data structures required by your application.

### Use sort order
Related items can be grouped together and queried efficiently if their key design causes them to sort together. 

### Distribute queries
It is also important that a high volume of queries not be focused on one part of the database, where they can exceed I/O capacity. Instead, you should design data keys to distribute traffic evenly across partitions as much as possible, avoiding "hot spots."

### Use global secondary indexes
By creating specific global secondary indexes, you can enable different queries than your main table can support, and that are still fast and relatively inexpensive.
