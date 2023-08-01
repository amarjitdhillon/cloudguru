

- A placement group is concerned primarily with network throughput and reducing latency among EC2 instances within a single availability zone. AWS does support a placement group spanning multiple AZs via spread placement groups, but unless “spread” is specifically mentioned, you should assume the question references a “normal” (or “cluster”) placement group.
- Cluster placement group is the default type of placement group.
- Spread placement groups can span availability zones and support up to 7 instances per zone.