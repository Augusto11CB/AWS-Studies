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

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

#### Partition Key + Sort Key (HASH + RANGE)

* The combination must be unique for each item.
* Data is grouped by partition key.
* Example: users-games table, “User\_ID” for Partition Key and “Game\_ID” for Sort Key.

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

### DynamoDB - Read/Write Capacity Modes

Note: You can switch between different modes once every 24 hours.

#### Provisioned Mode (default)

* You specify the number of reads/writes per second.
* You need to plan capacity beforehand.
* Pay for provisioned read & write capacity.
* Read Capacity Units (RCU) – throughput for reads.
* Write Capacity Units (WCU) – throughput for writes.
* Option to setup **auto-scaling** of throughput to **meet demand**.
* Throughput can be exceeded temporarily using “**Burst Capacity**”.
  * If Burst Capacity has been consumed, you’ll get a `ProvisionedThroughputExceededException`.
  * It’s then advised to do an exponential backoff retry.

**Console - Provisioned Mode With Auto Scaling Enabled**

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

**Console - Provisioned Mode With Auto Scaling Disabled**

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

#### On-Demand Mode

* Read/writes automatically scale up/down with your workloads.
* No capacity planning needed.
* Pay for what you use, more expensive (\$$$).





