# Cognito Identity Pools

### Cognito Identity Pools (Federated identities)

* Goal of this service: Get identities for “users” so they obtain temporary AWS credentials.
  * A Guest Policy can be defined and AWS credentials can be given to our guest users.
* Users can be allowed to log in through a trusted third party using this identity pool. Your identity pool (e.g identity source) can include:
  * This could be a public provider, for example, log in with Amazon, Facebook, Google, and Apple.
  * Users that are already logged in with the Amazon Cognito user pool can be allowed.
  * OpenID Connect Providers and SAML Providers can also be allowed.
* Once the users have obtained these AWS credentials, they **can access the AWS services directly with an API call using an SDK or through the API gateway**.
* These credentials that the users get have an IAM policy that is defined by what we do in Cognito Identity Pools and they can be customized based on the value of the user ID for fine-grained control.

<figure><img src="../../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

* Access to our private S3 Bucket and a DynamoDB Table is desired by web and mobile applications.
* The first step is to ensure that users get credentials of AWS, but the creation of IAM users for these applications is not desired.
* (1) Initially, a login and a token out of this login are to be obtained by the users.
  * Connection to a Cognito User Pool or to Google login, Facebook login for social identity providers or SAML or OpenID Connect will be allowed for our users.
  * A login with any of those will be done by them and a token will be obtained.
* (2) The Cognito Identity Pool service will be approached by them to exchange the token for temporary AWS credentials.
* (3) and (4) The login with whatever provider we have defined will first be verified by the identity pool.
* (5) Once it’s validated, the STS service will be approached by the Cognito Identity Pool to get temporary credentials for our web and mobile application users.
* (6) Once this is done, the credentials are returned to our applications and AWS can be accessed directly thanks to these credentials and the associated IAM policy.

#### How does Cognito Identity Pools decide which role to apply to which user?

* **Default IAM roles**: Amazon Cognito Identity Pools provide default IAM roles for both authenticated users and guest users. These roles define the permissions for user access to AWS resources.
* **Role selection based on user’s ID**: Rules can be defined to assign specific roles to each user, based on their unique ID. This allows for fine-grained access control and enhances security.
* **Partitioning user access**: By using <mark style="color:green;">**policy variables**</mark>, you can partition your users’ access to AWS resources. This means you can control which users have access to what resources, providing a high level of customization and security.

<figure><img src="../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

* **Obtaining IAM credentials**: Cognito Identity Pools obtain IAM credentials through the AWS Security Token Service (STS). This service provides temporary security credentials that applications can use to make AWS requests.
* **Trust policy of Cognito Identity Pools**: The IAM roles associated with your Cognito Identity Pool must have a “trust” policy for the identity pool. This policy allows the identity pool to assume the necessary roles and provide the appropriate permissions.
