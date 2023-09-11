# RDS, Aurora and ElastiCache

### AWS RDS

* RDS == Relational Database Service.
* It is a managed DB service for DB use SQL as query language.
* It allows you to create databases in the cloud that are managed by AWS.
  * Postgres
  * MySQL
  * MariaDB
  * Oracle
  * Microsoft SQL server
  * Aurora (AWS's DB)

#### Why RDS > DB on EC2?

* RDS is a managed service:
  * **Automated provisioning, OS patching**.
  * Continuous backups and restore to specific timestamp (point in time restore).
  * Monitoring dashboards.
  * **Read replicas** for improved read performance.
  * **Multi AZ setup** for  disaster recovery.
  * Maintenance windows for upgrades.
  * Scaling capability (vertical and horizontal).
  * Storage backed by EBS (gp2 or io1).
* BUT you **CANNOT** SSH into **your instances.**

#### **RDS Storage Auto Scaling**

* Helps to dynamically increase storage on the RDS DB instance.
* When RDS detects that the DB is running out of free space, it scales automatically.
* Avoid manually scaling your database storage.
  * :warning: A **maximum storage threshold** must be set.
* Amazon RDS starts a storage modification for an autoscaling-enabled DB instance when these factors apply (AWS, 2023a):
  * Free available space is less than or equal to 10% of the allocated storage.
  * The low-storage condition lasts at least five minutes.
  * At least six hours have passed since the last storage modification, or storage optimization has completed on the instance, whichever is longer.
* Useful for applications with unpredictable workloads.



#### RDS Read Replicas

* Up to 15 Read Replicas
* **Replicas Possible Arrangement:**
  * Within AZ.
  * Cross AZ.
  * Cross Regions.
* Replication is ASYNC :exclamation:
* Replicas can be promoted to their own DB.
* Applications must updated the connection string to leverage read replicas.

<figure><img src="../../.gitbook/assets/image (36).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

#### RDS Read Replicas - Use Cases

1. You have a production database that is taking on normal load.
2. You want to run a reporting application to run some analytics.
3. You create a Read Replica to run the new workload there.
4. The production application is unaffected.

<figure><img src="../../.gitbook/assets/image (37).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

#### RDS Read Replicas - Network Cost :money\_with\_wings:

* :exclamation: For RDS Read Replicas within the same region, you don’t pay the fee where data goes from one AZ to another.

<figure><img src="../../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

#### RDS Multi AZ (Disaster Recovery)

* The replication is syncronous.
* One DNS name - It helps to automatically failover to the standby version in case of the mater db fails.
* **NOT USED FOR SCALING**

<figure><img src="../../.gitbook/assets/image (39).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

* When it is used?
  * Failover in case of loss of AZ.
  * loss of network, instance or storage failure.

#### RDS - From Single AZ to Multi-AZ

* &#x20;Zero downtime operation (no need to stop the DB.
* Just click on “modify” for the database.
* The following happens internally:&#x20;
  * A snapshot is taken.
  * &#x20;A new DB is restored from the snapshot in a new AZ.
  * Synchronization is established between the two databases.



### Amazon Aurora

* **Proprietary Technology:** Aurora is a proprietary technology developed by AWS and is not open sourced.
*   **Database Engine Support:** Aurora supports both Postgres and MySQL as Aurora DB, allowing your existing drivers to work seamlessly as if Aurora were a Postgres or MySQL database.


* **Performance:** Aurora is designed to be "AWS cloud-optimized" and offers significant performance improvements compared to MySQL on RDS, with a claimed 5x performance boost, and over 3x the performance of Postgres on RDS.
* **Storage Scalability:** Aurora's storage automatically grows in increments of 10GB, scaling up to an impressive 128TB of data.
* **Replication:** Aurora supports up to 15 read replicas, and its replication process is faster than traditional MySQL, with sub-10 ms replica lag.
* **High Availability (HA):** Aurora is inherently designed for high availability. Failover in Aurora is instantaneous, ensuring minimal downtime in case of primary instance failures.
* **Cost:** While Aurora offers superior performance and high availability, it comes at a higher cost compared to **Amazon RDS**, typically around **20% more expensive**. However, the efficiency and performance improvements may justify the cost for many users.

#### Amazon Aurora High Availability and Read Scaling

**Data Redundancy and Resilience:**

* Aurora ensures high data durability by replicating your data across multiple Availability Zones (AZs). Specifically, :exclamation::exclamation::exclamation:**it maintains six copies of your data across three AZs**.
  * For **write operations**, only :exclamation:**four out of the six copies** are needed. This redundancy ensures data consistency and durability even in the event of AZ failures.
  * For **read operations**, Aurora only requires :exclamation:**three out of the six copies**, allowing for efficient and low-latency read access.
  * Aurora employs self-healing mechanisms with peer-to-peer replication. In the event of data or instance failures, Aurora can automatically recover and maintain data integrity.
* **Instance Roles:**
  * In an Aurora cluster, there is **one primary instance responsible for handling write operations**. This instance ensures data consistency and integrity.
* **Automated Failover:**
  * Aurora provides automated failover capabilities for the primary (master) instance. In the event of a failure, Aurora can initiate a failover process and promote a read replica to the new primary instance in **less than 30 seconds**. This rapid failover minimizes downtime and ensures high availability.
* **Read Scalability:** Master + up to 15 Aurora Read Replicas serve reads.
* **Cross-Region Replication:**
  * Aurora offers support for Cross Region Replication, allowing you to replicate your Aurora database to a different AWS region for disaster recovery, data locality, or other purposes. This feature enhances the database's resilience and availability.

<figure><img src="../../.gitbook/assets/image (40).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

### Reference

* AWS. _Working with storage for Amazon RDS DB instances_. Amazon Web Services. Disponível em: [https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER\_PIOPS.StorageTypes.html](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER\_PIOPS.StorageTypes.html#USER\_PIOPS.Autoscaling). Acesso em: 11 set. 2023a.
