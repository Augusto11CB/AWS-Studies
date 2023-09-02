# EC2 Fundamentals

* EC2 = Elastic Compute Cloud = Infrastructure as a Service&#x20;
*   It mainly consists in the capability of :&#x20;

    * Renting virtual machines (EC2).
    * Storing data on virtual drives (EBS).
    * Distributing load across machines (ELB).
    * Scaling the services using an auto-scaling group (ASG).



### EC2 Sizing and Configuration Options

* OS: Linux, Windows or Mac OS.
* How much CPU.
* How much RAM.
* How Much storage space:
  * Network-attached (EBS & EFS).
  * Hardware (EC2 Instance Store).
* Network card: speed of the card, Public IP.
* Firewall rules: **security group.**
* Bootstrap script (configure at first launch).



### EC2 User Data

* It is possible to bootstrap our instances using an EC2 User data script.
* Bootstrapping means launching commands when a machine starts.
* That script in only run once at the instance first start.
* EC2 user data is used to automate boot tasks such as:
  * Installing updates.
  * Installing software.
  * Downloading common files from the internet.
  * Etc.
* The Ec2 User Data Script runs with the **root user.**

### Security Groups

* Security Groups are the fundamental of network security in AWS.
* They act as a "firewall".
* They control how traffic is allowed into or out of our EC2 Instances.
  1. ![](<../../.gitbook/assets/image (6).png>)
* Security groups only contain **allow** rules.
* Security groups rules can reference by IP or by security group.



**What does Security Group regulate?**

* Access to Ports.
* Authorised IP ranges.
* Control of inbound network (from other to the instance).
* Control of outbound network (from the instance to other).
* AWS Console example:
  * ![](<../../.gitbook/assets/image (7).png>)

#### Good to Know About Security Groups

* Can be attached to multiple instances.
* Locked down to a Region/VPC combination (need to recreate securitu group of you change the region or VPC).
* Does live "outside" the EC2 - if traffic is blocked the EC2 won't see it.
* It's good to maintain one separate security group for SSH access.
* If your application is not accessible (time out), then it's a security group issue.
* If your application gives a "connection refused" error, then it's an application error or it's not launched.
* All inbound traffic is **blocked** by default.
* All outbound traffic is **authorised** by default.

#### <mark style="background-color:yellow;">Classic ports to know</mark>

* 22 = SSH (Secure Shell) - Log into a Linux Instance.
* 21 = FTP (File Transfer Protocol) - Upload files into a file share.
* 22 = SFTP (Secure File Transfer protocol) - Upload Files using SSH.
* 80 = HTTP - access unsecured websites.
* 443 = HTTPS - access secured websites.
* 3389 = (Remote Desktop Protocol) - Log into a windows instance.
