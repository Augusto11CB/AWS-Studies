# Containers on AWS

* Amazon Elastic Container Service (Amazon ECS).
  * Amazon's own container platform.
* Amazon Elastic Kubernetes Service (Amazon EKS).
  * Amazon's managed Kubernetes (open source).
* AWS Farget.
  * Amazon's own serverless container platform.
  * Works with ECS and with EKS.
* Amazon ECR.
  * Store container images (\~ dockerhub).

### Amazon ECS

[Task Role vs. Task Execution Role](https://www.youtube.com/shorts/VQfRQ9gGYD4)

Launch Types: Farget, EC2

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

#### Amazon ECS - EC2 Launch Type

* Launch Docker containers on AWS = Launch **ECS Tasks** on **ECS Clusters.**
* :warning: EC2 Launch Type: you must provision & maintain the infrastructure (the EC2 instances).
* **Each EC2** Instance must **run the ECS Agent** to register in the ECS Cluster.
* AWS takes care of starting / stopping containers.

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

#### Amazon ECS - Fargate Launch Type

* You do **not provision the infrastructure** (no EC2 instances to manage.
* It is all Serverless.
* Create only task definitions.
* AWS runs ECS Tasks based on CPU/RAM needed.
* To scale, just increase the number of tasks. Simple - no more EC2 instances.

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

#### Amazon ECS - IAM Roles for ECS

* EC2 Instance Profile (:warning: EC2 Launch Type only):
  * Used by the ECS agent.
  * Makes API calls to ECS service.
  * Send container logs to CloudWatch Logs.
  * Pull Docker image from ECR.
  * Reference sensitive data in Secrets Manager or SSM Parameter Store.
* ECS Task Role:
  * Allows each **task to have a specific role.**
  * Use different roles for the different ECS Services you run.
  * Task Role is defined in the task definition.
* [Task Role vs. Task Execution Role](https://www.youtube.com/shorts/VQfRQ9gGYD4)

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

#### Amazon ECS - Load Balancer Integrations

* Application Load Balancer supported and works for most use cases.
* Network Load Balancer recommended only for high throughput / high performance use cases, or to pair it with AWS Private Link.
* :thumbsdown: Classic Load Balancer supported but **not recommended** (no advanced features – no Fargate)

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

#### Amazon ECS - Data Volumes (EFS)

* Mount EFS file systems onto ECS tasks.
* Works for both EC2 and Fargate launch types.
* Tasks **running in any AZ** will share the same data in the EFS file system.
* **Fargate + EFS = Serverless.**
* Use cases: persistent multi-AZ shared storage for your containers.

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

#### ECS Service Auto Scaling

* Amazon ECS Auto Scaling uses **AWS Application Auto Scaling.**
  * ECS Service Average CPU Utilization.
  * ECS Service Average Memory Utilization - Scale on RAM.
  * :thumbsup:ALB Request Count Per Target – metric coming from the ALB.

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption><p>Font: TBD</p></figcaption></figure>

* **Target Tracking** - scale based on target value for a specific CloudWatch metric.
* **Step Scaling** - scale based on a specified CloudWatch Alarm.
* **Scheduled Scaling** - scale based on a specified date/time (predictable changes).

#### EC2 Launch Type - Auto Scaling EC2 Instances

* Accommodate ECS Service Scaling by adding underlying EC2 Instances.
* **Auto Scaling Group Scaling.**
  * Scale your ASG based on CPU Utilization.
  * Add EC2 instances over time.
  *

      <figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption><p>Font: BUENO, 2023</p></figcaption></figure>
* **ECS Cluster Capacity Provider:**
  * Used to automatically provision and scale the infrastructure for your ECS Tasks.
  * Capacity Provider paired with an Auto Scaling Group.
  * Add EC2 Instances when you’re missing capacity (CPU, RAM…)
  * [Amazon ECS Cluster Auto Scaling with a Capacity Provider](https://www.youtube.com/watch?v=0j8D-be2J1k)

<div data-full-width="false">

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption><p>Font: DAVIS, 2023</p></figcaption></figure>

</div>

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

#### ECS Scaling - Service CPU Usage Example

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption><p>Font: BUENO, 2023</p></figcaption></figure>

#### ECS Rolling Updates

* When updating from v1 to v2, we can control how many tasks can be started and stopped, and in which order.
* Service's Task Config Update Screen (console):&#x20;
  * ![](<../../.gitbook/assets/image (15).png>)
  * min healthy percent: 500 and Max healthy percent: 100
    * ![](<../../.gitbook/assets/image (16).png>)
  * min healthy percent: 100 and Max healthy percent: 200
    * ![](<../../.gitbook/assets/image (17).png>)



#### Amazon ECS - Load Balancing (EC2 Launch Type)

* You must allow on the EC2 instance’s Security Group any port from the ALB’s Security Group:
  * :exclamation::exclamation::warning: My understanding: &#x20;
    * EC2s holds docker containers.
    * Docker containers are inside EC2. Althout the request are for the Docker container because it "lives" inside an EC2, so you need to set up permissions for the ALB to access the EC2 (that runs your container) to establish comunication. You set this permission in the Security Group of the EC2 instances working as capacity providers.



### References

DAVIS, Neal. _Amazon ECS Cluster Auto Scaling with a Capacity Provider_. \[Videoaula]. YouTube, 2023. Disponível em: <[https://www.youtube.com/watch?v=0j8D-be2J1k](https://www.youtube.com/watch?v=0j8D-be2J1k)>. Acesso em: 26 set. 2023.
