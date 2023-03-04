# Notes of AWS Certified Cloud Practitioner All-in-One Exam Guide (Exam CLF-C01)
By Daniel Carter

## 1. Becoming An AWS Certified Cloud Practitioner
In order to pass the AWS CCP Exam, a candidate will be expected to demonstrate the following:
- Explain the value of AWS Cloud services
- Understand and be able to explain the AWS Shared Responsibility Model
- Understand and be able to explain security best practices for **AWS accounts** and **management consoles**
- Understand how pricing, costs, and budgets are done within AWS, including the tools that AWS provides for monitoring and tracking them
- Be able to describe the core and popular AWS service offerings (storage, daabases, compute, network and development)
- Be able to recommend and justify which AWS core services would apply to real-world scenarios

---

### About the AWS CCP Exam
- AWS CCP consists of 65 questions with a 90-minute exam time limit.
- The exam consists of two types of questions
    - Multiple choice: Each question has four possible answers, only one of which is correct.
    - Multiple response: Each question has five or more possible answers, two or more of which are correct
    - Unscored content
    - Any unanswered question is scored by the exam as incorrect.
- In order to pass the exam, you neet to score of 700.

### AWS CCP Domain
- The exam is divided into **four different domains**
![](ccp-domains.png)

- The number of questions of each section will generally follow the weighted distribution of content for the exam, so you will get more questions from some sections and fewer than others to reflect this.

- Domain 1 - Cloud Concepts
  - It will introduce you to the AWS and the value it can bring to your organization
- Domain 2 - Security and Compliance
  - It focuses on how security is a primary focus for AWS across all services
- Domain 3 - Technology
  - It convers the technical aspects of the AWS Cloud. This includes the tools and utilities to get users up and running in AWS, as well as code development.
- Domain 4 - Billing and Pricing
  - It covers the many different pricing models that AWS offers across all their services, focusing on the unifying fact that costs are only incurred for resources that are provisioned and only while they are being used.

## 2. Cloud Concepts
In this chapter the following topics are discussed:
- Define the AWS Cloud and its value proposition
- Identity aspects of AWS Cloud Economics
- List the different cloud architecture design principles

---

### What is Cloud Computing?

The NIST Definition of Cloud Computing - NIST SP 800-145

> Cloud computing is **a model for enabling** ubiquitous, convenient, on-demand network **access to a shared pool of configurable computer resources** (e.g., networks, servers, storage, applications, and services) that can be rapidly provisioned and released with minimal management effort or service provider interaction. This cloud model is composed of five essential characteristics, three service models, and four deployment models.

### Computing Cloud Computing Concepts
- Cloud Application is an application that does not reside or run on a user's device, but rather is accessible via network (ISO/IEC 17788)
- Cloud application portability is the ability to migrate a cloud application from one cloud provider to another (ISO/IEC 17788)
- Cloud computing is a kind of network-accessible platform that delivers services from a large and scalable pool of systems, rather than dedicated physical hardware and more static configurations (ISO/IEC 17788)
- Cloud data portability is the ability to move data between cloud providers (ISO/IEC 17788)
- Cloud deployment model is how cloud computing is deliveryd through a set of particular cofigurations and features of virtual resources. The cloud deployment models are **public, private, hybrid and community** (ISO/IEC 17788)
- Multitenancy is the situation where multiple customers and applications running within the same environment but in a way that they are isolated from each other and not visible to each other but share the same resources (ISO/IEC 17788)
- **Cloud service customer** is the one that holds a business relationship for services with a cloud service provider (ISO/IEC 17788)
- **Cloud service user** is the one that interacts with and consumes services offered by a cloud services customer (ISO/IEC 17788)

### Key Cloud Computing Characteristics
1. On-demand self-service
    - Cloud services can be requested, provisioned, and put into use by the customer through automated means without the need to interact with a person.
2. Broad network access
    - All cloud services and components are accessible over the network and accessible in most cases through many different vectors.
3. Resource pooling
4. Rapid elasticity
   - With cloud computing being decoupled from hardware and with the programmatic provisioning capabilities, services can be rapidly expanded at any time additional resources are needed. 
5. Metered service
    - Depending on the type of service and cloud implementation, resources are metered and logged for billing and utilization reporting. This metering can be done in a variety of ways(storage, network, memory, processing)
6. Multitenancy

### The cloud computing enabler - Virtualization
Virtualization is what makes cloud computing. When a request is made by a cloud customer through an automated web portal or other similar system, resources are automatically allocated to a virtual machine from the large pool of resources.

### Cloud Service Categories
#### IaaS
Infrastructure as a Service (IaaS) is a cloud service category where infrastructure-level services are provided by a cloud service provider (ISO/IEC 17788).

AWS Services:
   - Amazon Elastic Compute Cloud (EC2)
   - Elastic Block Store (EBS)
   - Elastic Load Balancing

The capability provided to the consumer is to **provision processing, storage, networks**, and other fundamental computing resources **where the consumer is able to deploy and run arbitrary software**
    - Customer has no control over the the underlying cloud infrastructure
    - Customer has control over the O.S, storage and deployed applications

Benefits:
    - Scalability
    - Cost of ownership of physical hardware:  Within IaaS, the customer does not need to procure any hardware
    - High availability
    - Physical and logical security requirements: the cloud provider assumes the cost and oversight of the physical security of its data centers. Data is also protected by layers of logical network security and user access security
    - Location and access independence
    - Metered usage
    - Choice of hardware

#### PaaS
Platform as a Service (PaaS) is cloud service category where platform services are provided to the cloud customer, and the cloud provider is responsible for the system up to the level of the actual application (ISO/IEC 17788).

AWS Service:
    - Elastic Beanstalk
    - SageMaker

The capability provided to the customer is to **deploy** onto the cloud infrastructure **consumer-created or acquired applications** created using programming languages, libraries, services, and tools supported by the provider
    - Customer has no cotnrol over the underlying cloud infra such as network, servers, O.S, and storage
    - Customer has control over the deployed applications and configuration settings for the application-hosting environment.

Benefits:
   - Auto-scaling
   - Multiple host environments: With the cloud provider responsible for the actual platform, the **customer has a wide choice of operating systems and environments**. It allows test in different environment
   - Choice of environments
   - Flexibility:  In a traditional data center setting, application **developers are constrained by the offerings of the data center** and are locked into proprietary systems that make relocation or expansion difficult and expensive. With **those layers abstracted in a PaaS model**, the developers have enormous flexibility to move between providers and platforms with ease
   - Ease of Upgrades
   - Cost-effective: only systems that are actively and currently used incur costs
   - Ease Access
   - Licensing: Cloud provider is responsible for handling proper licensing of operating systems and platforms,

#### SaaS
Software as a Service (SaaS) is a Cloud service category in which a full application is provided to the cloud customer, and the cloud provider maintains responsibility for the entire infrastructure, platform, and application (ISO/IEC 17788).

Known services:
    - Gmail
    - Dropbox
    - iCloud

Benefits:
- Support costs and efforts
- Reduced overall costs 
- Licensing
- Ease of use and administration
- Standardization

### Cloud Deployment Models

#### Public Cloud
NIST SP 800-145 definition:

> The cloud infrastructure is provisioned for open use by the general public. It may be owned, managed, and operated by a business, academic, or government organization, or some combination of them. It exists on the premises of the cloud provider.

#### Private Cloud
NIST SP 800-145 definition:

> The cloud infrastructure is provisioned for exclusive use by a single organization comprising multiple consumers (e.g., business units). It may be owned, managed, and operated by the organization, a third party, or some combination of them, and it may exist on or off premises.

#### Community Cloud
NIST SP 800-145 definition:

> The cloud infrastructure is provisioned for exclusive use by a specific community of consumers from organizations that have shared concerns (e.g., mission, security requirements, policy, and compliance considerations). It may be owned, managed, and operated by one or more of the organizations in the community, a third party, or some combination of them, and may exist on or off premises.

It is comparable to a private cloud with the exception of multiple ownership and/or control versus singular ownership of a private cloud.

#### Hybrid Cloud
NIST SP 800-145 definition:

> The cloud infrastructure is a composition of two or more distinct cloud infrastructures (private, community, or public) that remain unique entities, but are bound together by standardized or proprietary technology that enables data and application portability (e.g., cloud busting for load balancing between clouds).

### The Cost-Benefit Analysis of the different kinds of "Clouds"

#### Resource Pooling and Cyclical Demands
With a traditional data center, an organization has to maintain sufficient resources to handle their highest load peaks, which demands much larger up-front hardware and ongoing support costs. However, organizations might have a cyclical nature to their system demands.

In the case mentioned above, a transition to the cloud would be a benefit, since the up-front cost would be far lower without having to build up a massive infrastructure from the outset.

In cases where a company has a steady load throughout the year and cyclical peak of demands are not a concern for the company, then a move to a cloud environment may not yield the same level of benefits.

#### Data Center Costs vs. Operational Expense Costs
With facilities, utilities systems staff, networking, storage, and all the components needed to run data center operations being the responsibility of the cloud provider, the focus is then shifted to management and oversight, as well as requirements for building and auditing. 

It is important for any organization thinking about moving to a cloud environment to fully assess the staff and talents they already have and whether they can adapt to the new demands and changing roles in a cloud environment.

#### Focus Change
Companies have operations and development staff. By moving to a cloud environment, the operations side will fundamentally change running systems to overseeing them.

A rush to a cloud environment could disrupt productivity; cause internal fighting; or even result in a significant loss of staff. However, a move to a cloud carries enormous benefits such as: 
- Developers can very easily take on new projects and try out new innovations with the ability to rapidly allocate resources
- change in culture as well
- ability to quickly start projects without the traditional wait times and costs for hardware procurement and configuration

#### Ownership and Control
When an organization owns their data centers and all the hardware, they get to set all the rules and have full control over everything.

In a cloud environment, the organization gives up direct control over operational procedures, system management, and maintenance, as well as upgrade plans and environment changes.

Major cloud providers such as AWS have enabled a heightened sense of ownership with the flexibility they offer for configurations and the broad range of options for resources. 
#### Cost Structure
**Costs are very predictable in a traditional data center**. An organization can appropriate funds for capital expenditures for hardware and infrastructure and then allocate appropriate staffing and resources to maintain the hardware and infrastructure over time.

In a cloud environment with metered pricing, costs are realized as resources are added and changed over time.  This can cause an unpredictable schedule of costs.

### Universal Cloud Concepts
- Interoperability: It is the ease with which one can move or reuse components of an application or service
- Elasticity and Scalability
    - They are similar concepts in terms of the **changing of resources allocated** to a system or application to meet current demands
    - **The difference between them relates to the manner in which the level of resources is altered**
    - Scalability the allocated resources are changed statistically to meet anticipated demands or new deployments in services
    - Elasticity adds the ability for the dynamic modification of resources to meet demands as they evolve (customer can set thresholds for when a cloud environment will automatically add or remove resources)
- Performance
- Availability and Resiliency
    - To remember the **difference** between availability and resiliency **is the extent to which a system is affected by outages** 
    - Availability pertains to the overall status if a system is up or down.
    - Resiliency pertains to the ability of a system to continue to function when some aspect or portions of it experience an outage
- Portability: It is the key feature that allows systems to easily and seamlessly move between different cloud providers
- Service Level Agreements (**SLA**): It spells out in clear terms the minimum requirements for uptime, availability, processes, customer service and support, security controls and requirements, auditing, reporting, etc
- Governance: Governance at its core involves assigning jobs, tasks, roles, and responsibilities and ensuring they are satisfactorily performed 

## 3. Security and Complience
In this chapter the following topics are discussed:
- Define the AWS Shared Responsibility Model
- Define AWS Cloud security and compliance concepts
- Identify AWS access management capabilities
- Identity resources for security support

### AWS Shared Responsibility Model
Cloud provider responsabilities:
- facilities
- redundancy
- physical security
- network cabling
- hardware components
- availability zones, edge locations

Beyond the layers of physical facilities and computing hardware, there are differing levels of responsibility based upon the cloud services model employed.
![](responsability-cloud-provider-cloud-customer-diagram.png)

The image above shows the areas of responsibility within a cloud implementation. The shaded areas represent the responsibility on the part of the cloud provider.

#### Manage Resources vs. Unmanaged
1. Managed resources are those where the cloud provider is responsible for the installation, patching, maintenance, and security of a resource.
2. Unmanaged resources are those hosted within a cloud environment, but where the customer bears responsibility for host functions. 
## AWS Core Services Overview
![](aws-core-services-overview.png)