# EC2 Instance Storage

### Elastic Block Store- EBS

#### What is an EBS Volume?

* An EBS Volume is a durable, block-level storage device that can be attached to an EC2 instance.
* EBS volumes persist **independently from** the running life of an **EC2** instance, and when you create an EBS volume.
* It is **automatically** **replicated** within its **Availability Zone** to prevent data loss due to failure of any single hardware component.
* EBS volumes are particularly **well-suited** for use as the primary storage **for data that requires frequent updates**, such as the system drive for an instance or storage for a database application.&#x20;

> Think of them as a "network USB stick" (MAAREK, 2023).

* It is a network drive (i.e. not a physical drive):
  * It uses the network to communicate the instance, which means there might be a bit of latency.
  * It can be detached from an EC2 instance and attached to another one quickly.
* Have a provisioned capacity (size in GBs and IOPS).
  * You get billed for all the provisioned capacity.
  * You can increase capacity of the drive over time.

#### EBS - Delete on Termination Attribuite

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

* Controls the EBS behaviour when an EC2 instance terminates:
  * By default, the root EBS volume is deleted (attribute enabled).
  * By default, any other attached EBS volume is not deleted (attribute disabled).
* **\[Exam Question] Use case: preserve root volume when instance is terminated.**

### EBS Snapshots

* Make a backup (snapshot) of your EBS volume at a point in time.
* Not Necessary to detach volume to do snapshot, but recommended.
* Can Copy snapshots across AZ or Region.

<figure><img src="../../.gitbook/assets/image (8).png" alt="" width="557"><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

#### EBS Snapshots Features

* EBS Snapshot Archive:
  * Move a snapshot to an "archive tier" that is 75% cheaper.
  * Takes within 24 to 72 hours for restoring the archive.
* Recycle Bin for EBS Snapshots:
  * Setup rules to retain deleted snapshots so you can recover them after an accidental deletion.
* Fast Snapshot Restore (FSR):
  * Force full initialization of snapshot to have no latency on the first use (\$$\$$$).

### EBS Multi-Attach (`io I` and `io 2` family)

* Attach the same EBS volume to multiple EC2 instances in the same **AZ.**
* Each instance has full read & write permissions to the high-performance volume.
* **Use case:**
  * Achieve higher application availability in clustered Linux applications (ex: Teradata).
  * Applications must manage concurrent write operations.
* **\[Exam Question]** **UP TO 16 EC2 INSTANCES AT A TIME**
* Must use a file system that's cluster aware (not XFS, EXT4, etc).
