AWS Storage Gateway is a hybrid cloud storage service that gives you on-premises access to virtually unlimited cloud storage. Customers use Storage Gateway to simplify storage management and reduce costs for key hybrid cloud storage use cases.

## Types based on installation
They are of two types
1. It can be installed as VM on a hypervisor.
1. It comes as a physical box.

## Sharing Protocols
Two types of file sharing protocols are:

- `SMB`: Made by IBM originally and then taken by Microsoft. It is best used for Windows.
- `NFS`: Made by Sun. It can be used both with SMB and NFS.

## Types of Storage GW's
3 different types of fo storage gateways are:

- `File gateway (using NFS)`: The File Gateway presents a file interface that enables you to store files as objects in Amazon S3 using the industry-standard NFS and SMB file protocols, and access those files via NFS and SMB from your datacenter or Amazon EC2, or access those files as objects with the S3 API.

- `Volume Gateway`: The Volume Gateway presents your applications block storage volumes using the iSCSI protocol. Data written to these volumes can be asynchronously backed up as point-in-time snapshots of your volumes, and stored in the cloud as Amazon EBS snapshots.
Tape Gateway: Used to backup data into the glacier.

- `Cached volumes`: Entire dataset is stored on S3 and the most frequently used data is cached on-prem


## Notes

- Snapshots are incremental backups (delta) which will only capture the changed blocks. 
- In the case of stored volume all the data is stored on the data center (on-prem) and  the data is replicated  to the backend server in an `Async` fashion
- VM is used to replicate the data


