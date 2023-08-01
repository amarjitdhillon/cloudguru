# Elastic File System

- Sun created NFS (which is a distributed File System)
- EFS is an implementation for NFS file share
- The storage capacity is elastic.
- It is a great way of sharing the files between the two instances.
- EFS uses the NFS file system.
- Unlike the EBS where we have to define/provision space, in the EFS we do not need to - do that as they are backed by S3.
- It can scale up to Petabytes.
- It can support thousands of concurrent EFS connections.
- Data is stored across multiple AZ’s in a region.
- Read after write consistency.


## When to use which one?

1. EFS: for Linux based systems that need the distributed storage.
1. Amazon FSx for Windows: When you need storage for windows-based systems for Sharepoint, SQL Server, etc.
1. Amazon FSx for Lustre: for HPC and ML in windows env. It can store data on S3.

