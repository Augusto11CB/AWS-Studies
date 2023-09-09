# ELB and ASG

* ELB = Elastic Load Balancer
* ASG = Auto Scaling groups

### Why Use a Load Balancer?

* Spread load across multiple downstream instances.
* Expose a single point of access (DNS) to your application.
* Seamlessly handle failures of downstream instances.
* Do regular health checks to your instances.
* Provide SSL termination (HTTPS) for your website.
* Enforce stickiness with cookies.
* High availability across zones.
* Separate public traffic from private traffic.

### AWS Elastic Load Balancer (ELB)

* An Elastic Load Balancer is a managed load balancer.
  * AWS guarantees that it will be working.
  * AWS takes care of upgrades, maintenance, high availability.
  * AWS provides only a few configuration knobs.
* It is integrated with many AWS services:
  * EC2, EC2 ASG, ECS.
  * ACM, CloudWatch.
  * Route 53, AWS WAF. AWS Global Accelerator.

#### Types of Load Balancer on AWS

* AWS has 4 kinds of managed Load Balancers
* ~~Classic Load Balancer (v1 - old generation) - 2009 - **CLB**~~:
  * HTTP, HTTPS, TCP, SSL (secure TCP).
* Application Load Balancer (V2 - new generation) - 2016 - **ALB**:
  * HTTP, HTTPS, WebSockets.
  * Layer 7
* Network Load Balancer (v2 - new generation) - 2017 - **NLB**:
  * TCP, TLS (secure TCP, UDP).
  * Layer 4
* Gateway Load Balancer - 2020 - GWLB
  * Operates at layer 3 (Network Layer) - IP Protocol.
* LBs can be setup as internal (private) or external (public) ELBs.

#### Load Balancer Security Groups

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

**Load Balancer's Security Group:**

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

* Users can access load balancer from anywhere using HTTP or HTTPS.

**Application's Security Group:**

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

* Allow traffic only from Load Balancer.
* The source of it is the Load Balancer's Security Group (sg-054b5ff5ea02f2b6e)



### Application Load Balancer

* Application load balancers is Layer 7 (HTTP).
* Load balancing to multiple HTTP applications across machines (**target groups**).
* • Load balancing to multiple applications on the same machine (ex: containers).
* Support for HTTP/2 and WebSocket.
* Support redirects (from HTTP to HTTPS for example).
* Routing tables to different target groups:
  * Routing based on path in URL (example.com/**users** & example.com/**posts**).
  * Routing based on hostname in URL (**one.example.com** & **other.example.com**).
  * Routing based on Query String, Headers (example.com/users?**id=123\&order=false**).
* Has a port mapping feature to redirect to a dynamic port in ECS.

#### Target Groups

* EC2 instances (can be managed by an Auto Scaling Group) – HTTP.
* ECS tasks (managed by ECS itself) – HTTP.
* Lambda functions – HTTP request is translated into a JSON event.
* IP Addresses – must be private IPs.
* ALB can route to multiple target groups.
* **Health checks are at the target group level**.

#### ALB Good to Know

* Fixed hostname (XXX.region.elb.amazonaws.com).
* The application servers don’t see the IP of the client directly.
  * • The true IP of the client is inserted in the header `X-Forwarded-For`.
  * We can also get Port (`X-Forwarded-Port`) and proto (`X-Forwarded-Proto`).



### Network Load Balancer

* Network load balancers (Layer 4) allow to:
  * Forward TCP & UDP traffic to your instances.
  * Handle millions of request per seconds.
  * Less latency \~100 ms (vs 400 ms for ALB).
* :exclamation::exclamation:**NLB has one static IP per AZ, and supports assigning Elastic IP.**
  * helpful for whitelisting specific IP.
* Not included in the AWS free tier.

#### Target Groups

* EC2 Instances.
* IP Addresses (must be private IPs).
* Application Load Balancer.
* Health Checks support the TCP, HTTP and HTTPS Protocols.

<figure><img src="../../.gitbook/assets/image (26).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

### Gateway Load Balancer

* Deploy scale, and manage a fleet of 3 party network virtual appliances in AWS.
* Example:
  * Use a Gateway Load Balancer if you want, **AT NETWORK LEVEL**, to have all of your network's traffic go through:
    * a **firewall** that you have.
    * an intrusion detection and prevention system (IDPS).
    * deep packet inspection system.
    * **payload manipulation**.

<figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

* &#x20;Uses the **GENEVE** protocol on port 6081
* Operates at Layer 3 (Network Layer) – IP Packets.
* Combines the following functions:
  * Transparent Network Gateway – single entry/exit for all traffic.
  * Load Balancer – distributes traffic to your virtual appliances

#### Target Groups

* EC2 Instances.
* IP Addresses (must be private IPs).

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>





### ELB Sticky Sessions (Session Affinity)

* It is possible to implement stickiness by using "_**cookies**_" so that the same client is always redirected to the same instance behind a load balancer.
* This works for Classic Load Balancer, **Application Load Balancer**, and **Network Load Balancer**.
* For both CLB & ALB, the “**cookie**” used for stickiness has an expiration date you control.
* Use case: make sure the user doesn’t lose his session data.
* :warning:Enabling stickiness may bring **imbalance** to the load over the backend EC2 instances.

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>



#### Cooki

#### Cookie Names

There are two type of cookie that can be use for sticky sessions.

**(1) Application-based cookies**

There are two kind of cookies in this within the application-basesd cookies (custom cookie and application cookie).

* Custom Cookie:
  * Generated by the target (application).
  * Can include any custom attributes required by the application.
  * Cookie name must be specified individually for each target group.
  * Must not use the following names: AWSALB, AWSALBAPP, AWSALBTG (they are reserved for use by the ELB).
* Application Cookie:
  * Generated by the load balancer.
  * Cookie name is AWSALBAPP.

**(2) Duration-Bases Cookies**

* Cookie generated by the Load Balancer.
* Cookie name is AWSALB for ALB, AWSELB for CLB.
* :exclamation:The expiration duration is generated by the load balancer itself.



<figure><img src="../../.gitbook/assets/image (24).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>



### Cross-Zone Load Balancing

Cross-Zone Load Balancing is an option for load balancers on AWS that allows them to distribute traffic across the registered targets in all enabled Availability Zones, instead of only within the same Availability Zone (AWS, 2023a).&#x20;

This means that if one Availability Zone has more traffic than another, the load balancer can balance the load by sending some requests to the targets in the less busy Availability Zone (AWS, 2023a).

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

* ALB&#x20;
  * :bangbang:Enabled by default (can be disabled at the Target Group level).
  * No charges for inter AZ data
* NLB and GLB
  * Disabled by default.
  * You pay charges ($) for inter AZ data if enabled.

#### Cross-Zone for ALB

Feature enabled by default in the ALB.

<figure><img src="../../.gitbook/assets/image (25).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

In order to turn this feature off:

(1) go to the ALB target group.

<figure><img src="../../.gitbook/assets/image (28).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

(2) go to attributes and edit it.

<figure><img src="../../.gitbook/assets/image (29).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (30).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (31).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>



### Load Balancer - SSL Certificates

* The load balancer uses an X.509 certificate (SSL/TLS server certificate).
* You can manage certificates using **ACM** (AWS Certificate Manager).
* You can create upload your own certificates alternatively.
* HTTPS Listener:
  * You must specify a default certificate.
  * You can add an optional list of certs to support multiple domains.
  *   Clients can use SNI (Server Name Indication) to specify the hostname they reach.

      * More about SNI in: [Server Name Indication (SNI)](http://127.0.0.1:5000/s/XWfI2QGLeclVUrQb9PYi/server-name-indication-sni "mention")
      * Only works for ALB, NLB, and CloudFront.



      <figure><img src="../../.gitbook/assets/image (21).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>



### Connection Draining (Deregistration Delay)

* Feature naming
  * Connection Draining - CLB
  * Deresgistration Delay - ALB and NLB
* :exclamation:Time to complete "in-flight requests" while the instance is de-registering or unhealthy.
* Stops sending new requests to the EC2 instance which is de-registering.
* Between 1 to 3600 seconds (default: 300 seconds).
* Can be disablet (set value to 0).

<figure><img src="../../.gitbook/assets/image (23).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>



### Auto Scaling Group (ASG)

<figure><img src="../../.gitbook/assets/image (32).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

###

###

###

### References

* AWS. Cross-zone load balancing. Amazon Web Services. Disponível em: [https://docs.aws.amazon.com/elasticloadbalancing/latest/network/network-load-balancers.html](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/network-load-balancers.html#cross-zone-load-balancing). Acesso em: 9 set. 2023a.



