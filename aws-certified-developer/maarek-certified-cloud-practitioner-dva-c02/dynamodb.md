# DynamoDB

* Fully managed, highly available with replication across multiple AZs.&#x20;
* NoSQL database - not a relational database.
* Scales to massive workloads, distributed database.
* Millions of requests per seconds, trillions of row, 100s of TB of storage.
* Fast and consistent in performance (low latency on retrieval).
* Integrated with IAM for security, authorization and administration.
* Enables event driven programming with DynamoDB Streams.
* Low cost and auto-scaling capabilities.
* Standard & Infrequent Access (IA) Table Class.

***

* DynamoDB is made of Tables.
* Each table has a **Primary Key** (must be decided at creation time).
* Each table can have an infinite number of **items** (= **rows**).
* Each item has **attributes** (can be added over time – can be null).
* Maximum size of an item is 400KB.
* Data types supported are:
  * **Scalar Types** - String, Number, Binary, Boolean, Null.
  * **Document Types** - List, Map.
  * **Set Types** - String Set, Number Set, Binary Set.



### DynamoDB - Primary Keys

#### Partition Key (HASH)

* Partition key must be unique for each item.
* Partition key must be “diverse” so that the data is distributed.

<figure><img src="../../.gitbook/assets/image (3) (1).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

#### Partition Key + Sort Key (HASH + RANGE)

* The combination must be unique for each item.
* Data is grouped by partition key.
* Example: users-games table, “User\_ID” for Partition Key and “Game\_ID” for Sort Key.

<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

### DynamoDB - Read/Write Capacity Modes

Note: You can switch between different modes once every 24 hours.

#### Provisioned Mode (default)

* You specify the number of reads/writes per second.
* You need to plan capacity beforehand.
* Pay for **provisioned** read & write capacity.
* Read Capacity Units (RCU) – throughput for reads.
* Write Capacity Units (WCU) – throughput for writes.
* Option to setup **auto-scaling** of throughput to **meet demand**.
* Throughput can be exceeded temporarily using “**Burst Capacity**”.
  * If Burst Capacity has been consumed, you’ll get a `ProvisionedThroughputExceededException`.
  * It’s then advised to do an exponential backoff retry.

**Console - Provisioned Mode With Auto Scaling Enabled**

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

**Console - Provisioned Mode With Auto Scaling Disabled**

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

#### On-Demand Mode

* Read/writes automatically scale up/down with your workloads.
* No capacity planning needed.
* Pay for what you use, more expensive (\$$$).
* Read/writes automatically scale up/down with your workloads.
* No capacity planning needed (WCU / RCU).
* Unlimited WCU & RCU, no throttle, more expensive.
* You’re charged for reads/writes that you use in terms of RRU and WRU.
* **Read Request Units (RRU)** - throughput for reads (same as RCU).
* **Write Request Units (WRU)** - throughput for writes (same as WCU).
* **2.5x more expensive than provisioned capacity (use with care).**
* Use cases: unknown workloads, unpredictable application traffic.

### DynamoDB - Write Capacity Units (WCU)

* One Write Capacity Unit (WCU) represents one write per second for an item up to 1 KB in size.
* If the items are larger than 1 KB, more WCUs are consumed.

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

### DynamoDB Strongly Consistent Read vs. Eventually Consistent Read.

* Eventually Consistent Read (default):
  * If we read just after a write, it’s possible we’ll get some stale data because of replication.
* Strongly Consistent Read:
  * If we read just after a write, we will get the correct data.
  * Set “ConsistentRead” parameter to True in API calls (GetItem, BatchGetItem, Query, Scan).
  * Consumes twice the RCU.

### DynamoDB - Read Capacity Units (RCUs)

* One Read Capacity Unit (RCU) represents one Strongly Consistent Read (SCR) per second, or two Eventually Consistent Reads (ECR) per second, for an item up to 4 KB in size.
* If the items are larger than 4 KB, more RCUs are consumed.

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

* Calculation involving Eventually Consistent Reads: ECR/2 \* ItemSize/4KB.
* Calculation involving Strongly Consistent Read: SCR \* ItemSize/4KB

### DynamoDB - Partitions Internal

* Data is stored in partitions.
* Partitions keys go through a hashing algorithm to know to which partition they go to.
* In DynamoDB, data is organized into tables, which are further divided into partitions. Partitions are the fundamental unit of scalability in DynamoDB. Each partition is stored on its own server to ensure high availability and fault tolerance. The number of partitions in a DynamoDB table is initially determined based on the table's provisioned throughput.
* WCUs and RCUs are spread evenly across partitions.
* :warning: :warning: :warning: :warning: :warning: :warning: If you have 10 partitions, and you provide a new provision with 10 **WCUs** and 10 **RCUs**, then they're going to be spread evenly across partitions.
  * The even distribution of capacity ensures that the workload is spread across the partitions, preventing hotspots where certain partitions become overloaded with requests while others remain underutilized. DynamoDB's automatic partition management takes care of distributing the data and load balancing the requests to provide optimal performance and scalability.

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

### DynamoDB - Throttling

* If we exceed provisioned RCUs or WCUs, we get "ProvisionedThroughputExceeded Exception.
* Reasons:
  * Hot Keys (e.g., popular item).
  * Hot partitions.
  * Very Large items.
*
