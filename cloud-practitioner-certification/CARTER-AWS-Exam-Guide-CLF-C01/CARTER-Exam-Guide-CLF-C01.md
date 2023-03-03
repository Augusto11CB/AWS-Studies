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
#### Data Center Costs vs. Operational Expense Costs
#### Focus Change
#### Ownership and Control
#### Cost Structure

