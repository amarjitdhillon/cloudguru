

- If all your clients are in one region, then there is little advantage to adding read replicas to additional regions. Instead, providing replicas in the same region as the clients gives them the fastest access.

- You also cannot failover to a read replica. You can convert it to a stand-alone instance, but that is a manual process that is not a failover.