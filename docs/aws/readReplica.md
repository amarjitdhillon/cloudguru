# Read Replicas

- A multi-AZ instance can not be promoted to a read-replica.
- There is no charge for primary-to-secondary data replication.
- Although it’s not particularly common, you can set up a read replica in an on-premises instance. Additionally, read replicas are often created in separate regions from the primary instance, to improve performance for clients closer to different regions than the primary instance.
- ==Currently, read replicas in RDS are only supported by MariaDB, MySQL, and PostgreSQL. Not for DynamoDB==
- Read replicas are updated via asynchronous replication—  the most performant approach.
- Read replica setup only allows for five read replicas. This is not a limit that can be raised by AWS.
- Read replica has its own database engine active so that it can be promoted to a primary DB.
- Multi-AZ setup is focused on disaster recovery and fault tolerance, while read replicas provide performance and scalability.
- You can manually promote (not automatically ) a read replica instance to a stand-alone instance if you have to.
- Read replicas do not create automatic backups, but the primary database instance must have automatic backups enabled to create read replicas.

!!! tip
  - There is no particular performance increase in a Multi-AZ deployment unless read replicas are also turned on.