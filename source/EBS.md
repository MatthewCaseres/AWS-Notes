# EBS

## What is EBS?

EBS lets EC2 instances have persistent storage that doesn't go away when the instance stops, hibernates, or is terminated. EBS is like an external hard-drive for your EC2 instances. This is in contrast to EC2 **instance store volumes** which store temporary data on the same host computer.

The EBS volumes are not on the same host computer but instead are attached by the network. However, EBS volumes are specific to availability zone. The average latency between EC2 instances and EBS is single digit milliseconds.

![](./images/ec2-storage-partial.png)

## Instance Types

The main instance types are:

- Solid state drives (SSD) — Optimized for transactional workloads involving frequent read/write operations with small I/O size, where the dominant performance attribute is IOPS. The two types of SSD backed volumes are:
  - **General Purpose SSD** (**gp2** and **gp3**): a balance of price and performance. We recommend these volumes for most workloads.
  - **Provisioned IOPS SSD** (**io1** and **io2**) - Provides high performance for mission-critical, low-latency, or high-throughput workloads.
    - Amazon EBS Multi-Attach enables you to attach a single Provisioned IOPS SSD (io1 or io2) volume to multiple instances that are in the same Availability Zone.
    - Multi-attach only works for Nitro-enabled instances and io1 or io2. Nitro is providing some sort of hardware support. Up to 16 instances.
    - EBS Block Express is the next generation of Amazon EBS storage server architecture. It has been built for the purpose of meeting the performance requirements of the most demanding I/O intensive applications that run on Nitro-based Amazon EC2 instances. io2 Block Express volumes are suited for workloads that benefit from a single volume that provides sub-millisecond latency, and supports higher IOPS, higher throughput, and larger capacity than io2 volumes.
- Hard disk drives (HDD) — Optimized for large streaming workloads where the dominant performance attribute is throughput. The two types of HDD backed volumes are:

  - **Throughput Optimized HDD (st1)** — A low-cost HDD designed for frequently accessed, throughput-intensive workloads.
  - **Cold HDD (sc1)** — The lowest-cost HDD design for less frequently accessed workloads.

  <!-- TODO: Discuss IOPS in more precision -->

## Snapshots

You can create point-in-time snapshots of EBS volumes, which are persisted to Amazon S3. Snapshots protect data for long-term durability, and they can be used as the starting point for new EBS volumes. The same snapshot can be used to instantiate as many volumes as you wish.

## Encryption

You can expect the same IOPS performance on encrypted volumes as on unencrypted volumes, with a minimal effect on latency. You can access encrypted volumes the same way that you access unencrypted volumes. Encryption and decryption are handled transparently, and they require no additional action from you or your applications.

When you create an encrypted EBS volume and attach it to a supported instance type, the following types of data are encrypted:

- Data at rest inside the volume
- All data moving between the volume and the instance
- All snapshots created from the volume
- All volumes created from those snapshots

EBS encrypts your volume with a data key using the industry-standard AES-256 algorithm.

[EBS Volume Types docs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volume-types.html)

https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AmazonEBS.html

https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html
