# IAM and AWS CLI

* IAM = Identity and Access Management.
* IAM is a Global Service.
* Users: are people within your organization, and can be grouped.
* Groups: only contain users, not other groups.

<figure><img src="../../.gitbook/assets/image (9) (1).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

### IAM Permissions

* IAM Permissions define the permissions of the users.

### IAM Policies

* IAM Policies are JSON documents that define a set of permissions for making requests to AWS services, and can be used by IAM Users, User Groups, and IAM Roles.
* <mark style="color:orange;">**Inline policy**</mark>
  * An inline policy is an IAM policy that is created for a single IAM identity, such as a user.&#x20;
  * Inline policies maintain a strict one-to-one relationship between the policy and the identity to which it is applied. This means that when you delete the user in which the inline policy is embedded, the policy will also be deleted.

#### IAM Policies Structure

<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

### IAM Roles

* Some AWS services will need to perform actions on your behalf.
* Todo so, we will assign permissions to AWS services with **IAM Roles**.&#x20;

<figure><img src="../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>

#### Who can have a IAM Role?

<figure><img src="../../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption><p>Font: AWS Console, 2023</p></figcaption></figure>

* **AWS Services**
* AWS Accounts
* Web identity
* SAML 2.0 Federation
* Custom Trust Policy

### IAM Security Tools

* IAM Credentials Report (account-level)
  * Tool that generates a report that lists all account's users and the status of their various credentials.
* IAM Access Advisor (user-level)
  * Tool that **shows the service permissions granted to a user** and when those services were last accessed.



### IAM Section - Summary

* Users: mapped to a physical user, has a password for AWS Console.
* Groups: Contains users only.
* Policies: JSON documente that outlines permissions for users or groups.
* Roles: The way to assign permissions to AWS Services.
* Security: MFA + Password Policy
* AWS CLI: Manage AWS Services using command-line.
* AWS SDK: Manage AWS services using a programming language.
* Access Keys: Access AWS using the CLI or SDK.
* **Audit:** IAM Credentials Reports & IAM Access Advisor.



### Security Groups

* Security Groups are the fundamental of network security in AWS.
*   They control **how traffic is allowed into or out** of Ec2 Instances.





    <figure><img src="../../.gitbook/assets/image (5) (1) (1).png" alt=""><figcaption><p>Font: MAAREK, 2023</p></figcaption></figure>
* Security groups only contain **allow** rules;
* Security groups rules **can reference** by **IP** or by **security group**

