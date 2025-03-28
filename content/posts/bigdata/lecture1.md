

+++
date = '2025-03-27T22:11:14-04:00'
draft = true
title = 'Big Data Technologies: Lecture 1'
+++

# Big Data Technologies: Understanding the Fundamentals

## What is Big Data?

Big Data refers to data sets that are too large or complex to be dealt with by traditional data processing applications. Today's digital landscape generates unprecedented volumes of data:

- Platforms like Facebook and Instagram generate **terabytes of data daily** through images, videos, text, and user interactions
- IoT devices continuously stream data from millions of sources
- Business transactions produce massive logs requiring real-time analysis
- Scientific instruments and experiments generate enormous datasets

To effectively store, process, and analyze such massive datasets, specialized Big Data technologies are required.

## The 4 V's of Big Data

Big Data is commonly characterized by four key dimensions:

1. **Volume**: The sheer quantity of data being generated (terabytes, petabytes, or even exabytes)
2. **Velocity**: The speed at which data is being generated, collected, and processed
3. **Variety**: The diversity of data types and sources (structured, semi-structured, unstructured)
4. **Veracity**: The reliability and accuracy of data, considering inconsistencies and uncertainties

## The Need for Distributed Processing

**Traditional Processing Example:**
- 1 TB data
- Single node with 4 I/O ports
- Each port processes at 100 MB/s
- Total processing rate: 400 MB/s
- Time required: 1000 GB ÷ 0.4 GB/s = 2,500 seconds ≈ 42 minutes

**Hadoop Distributed Processing:**
- Same 1 TB data distributed across 10 nodes
- Each node has 4 I/O ports at 100 MB/s
- Total processing rate: 4,000 MB/s
- Time required: 1000 GB ÷ 4 GB/s = 250 seconds ≈ 4.2 minutes

This 10x improvement in processing time demonstrates the power of distributed computing for Big Data workloads.

## Hadoop Distributed File System (HDFS)

HDFS is designed to reliably store very large files across machines in a large cluster.

**Key Characteristics:**
- **Write-once, read-many**: Files in HDFS are write-once and support multiple reads
- **Fault tolerance**: Automatically replicates data across multiple nodes
- **High throughput**: Optimized for large, sequential read operations
- **Commodity hardware**: Designed to run on low-cost hardware

## HDFS Write Anatomy

![HDFS Write Process](/hdfswrite.png)

1. **Create**: Client creates a file using the distributed file system API, making an RPC (Remote Procedure Call) to the NameNode to create a new file. The NameNode verifies user permissions and checks if the file already exists.

2. **Write**: When the client begins writing data, the DFSOutputStream splits it into packets. These packets form a data queue that is consumed by the DataStreamer.

3. **Replication**: By default, `dfs.replication = 3`, meaning each block of data is written to three DataNodes to ensure fault tolerance.

4. **Acknowledgment**: When each data packet is successfully stored on all three DataNodes, they return acknowledgment packets to the client.

5. **Failure Handling**: If any DataNode fails during the write process, it is removed from the pipeline and a new data pipeline is created using the remaining nodes. The failed block is marked as "under-replicated."

6. **Rack Awareness**: HDFS is rack-aware, meaning it distributes replicas across different racks to improve fault tolerance against rack failures.

## HDFS Read Anatomy

![HDFS Read Process](/readNode.png)

1. **Verification**: During reading, the DFSInputStream verifies checksums to ensure data integrity.

2. **Location Discovery**: The client issues an open() method call, and DFS contacts the NameNode. The NameNode provides information about which DataNodes contain the requested blocks.

3. **Optimization**: HDFS optimizes reads by selecting the closest DataNode that contains the requested data, minimizing network traffic.

## HDFS Architecture Components

### NameNode

The NameNode is the central component of HDFS that manages the filesystem namespace:

- Maintains the filesystem tree and metadata for all files and directories
- Maps blocks to DataNodes
- Represents a potential single point of failure (SPOF)
- Stores metadata in two critical files:
  - **FSImage**: A point-in-time snapshot of the filesystem metadata
  - **EditLog**: A transaction log recording all changes to filesystem metadata

![NameNode Operation](/namenode.png)

When the NameNode starts up, it merges the FSImage with the EditLog to create a consistent view of the filesystem. If the EditLog is large, the NameNode startup time increases significantly.

### Secondary NameNode

The Secondary NameNode helps the primary NameNode manage its metadata:

- It's **not** a backup or standby replacement for the primary NameNode
- Periodically merges the FSImage and EditLog to create a new, updated FSImage
- Reduces the NameNode restart time by keeping the EditLog size manageable
- Typically runs on a separate machine to avoid resource competition

### High Availability in Hadoop 2+

In Hadoop 2 and later versions, high availability is implemented with:

- **Active NameNode**: Serves client requests
- **Standby NameNode**: Maintains an up-to-date copy of the namespace
- Automatic failover to the Standby NameNode if the Active NameNode fails

This architecture eliminates the single point of failure present in earlier Hadoop versions.

## Key Takeaways

- Big Data requires specialized technologies for efficient storage and processing
- Hadoop provides a distributed framework for handling large-scale data operations
- HDFS offers reliable, redundant storage with optimized read/write operations
- Understanding NameNode architecture is crucial for managing Hadoop clusters
- High availability features are essential for production Hadoop deployments


In the [next lecture]({{< ref "lecture2.md" >}}), we'll explore MapReduce - the computational model that works with HDFS to process data in a distributed manner.