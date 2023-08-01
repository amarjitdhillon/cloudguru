<!-- <center> <img src="../images/ebs/ebs-basic.jpg" width="90%"> </center> -->

- We can think them of to be like `virtual hard drives`
- They can only be used with EC2
- Can only be tied to single AZ
- Officially, instances can have up to 28 EBS attachments. One of those attachments is the network interface attachment, leaving 27 attachments available for EBS volumes. However, the better approach is to remember that an instance can attach to a root volume and several more volumes (more than two).

------

As shown in the image below, the EC2 instance storage is locked to EC2 instance while EBS are not locked to an EC2. We can also create snapshot from EBS

<center> <img src="../images/ebs/ebs-basic.jpg" width="90%"> </center>


!!! question 'Why do we need snapshots?'
    - Cost effective backup stragegy
    - To share data-sets with others users/accounts
    - Migrate a system to new AZ/Region
    - They are used to convert unencrypted volume to an encrypted one


Each EBS is replicated in it’s AZ by default.

## Encryption 

- EBS volumes can be encrypted when they are created.
- You cannot encrypt an existing EBS volume “on the fly.” You must create a snapshot and then encrypt that snapshot as you copy it to another, encrypted snapshot. You can then restore from that new snapshot.


!!! warning "What all is encrypted in EBS?"

    There are four types of data encrypted when an EBS volume is encrypted: 

        - Data at rest on the volume.
        - Data moving between the volume and the instance.
        - Any snapshots created from the volume.
        - Any volumes created from those snapshots.


!!! tip "Points to remember"
  - You must make a copy of an unencrypted snapshot to apply encryption.
  - You cannot encrypt an existing EBS volume.
  - You cannot encrypt a snapshot that is unencrypted.
  - You can encrypt a copy of a snapshot and restore an encrypted snapshot to a volume that is encrypted.

## Different types of EBS

- General-purpose SSD
- Provisioned IOPS SSD
- Throughput optimized HDD
- Cold HDD: Cold HDD is the lowest cost HDD
- EBS magnetic HDD


##  Move the EBS from one AZ to another 

### Option A
- creates a snapshot from a volume.
- create an AMI from a snapshot.
  
### Option B
- Copy the AMI to a different region. Then go to that region and choose the AZ
AZ’s can be changed when we choose from the subnets


## Types of root volumes
2 types of root volumes are there:

  1. `Instance storage` : They are called `Ephemeral storage` as we are going to lose all the data if it’s stopped. They can not be stopped.
  2. `EBS backed`: they can be stopped, they are persisted as well.

!!! error "Remember"
    By default, root volumes do get deleted when the associated instance terminates. However, you can configure this to not be the case.

- We can create AMI from both snapshots and volumes.
- For an EBS volume that is used as a root volume, if you want to take a consistent - snapshot then stop the instance as it is writing the data to EBS.
- ENI (Elastic Network Interface):
- EN (Enhanced Networking): This has a high speed of 100 Gbps and is used for high - performance. It uses the ENA (Enhanced network adapter).
- EFA (Elastic Fiber Adapter): use for HPC and ML.


!!! warning
    - If we close the instance, then the root volume is deleted but the persisted data - remains.
    - Volumes exist on EBS whereas the snapshots exist on S3
    - Snapshot is a delta (incremental). Taking the first snapshot may take a lot of time.
    - We can change the EBS volume size on the fly.
    - Volumes are always in the same AZ as the instance is.
    - We can create AMI from snapshots.
    - Move EC2 to at new AZ
    - take a snapshot → to create AMI → use AMI to launch in new AZ
    - Move EC2 to a new region
    - Take a snapshot → to create AMI → copy AMI to new region →  use AMI to launch in new - AZ