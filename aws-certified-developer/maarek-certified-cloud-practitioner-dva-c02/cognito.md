# Cognito

* If you are asking yourself, "Are users already present in IAM?", the answer is yes, they are.
  * Your web and mobile application users will be handled by Cognito, which is located outside of AWS.
  * Keywords to look for in the exam include "hundreds of users," "mobile users," and "authentication."
  * Mechanisms like SAML will be used for authentication.

### Cognito User Pools (CUP) - User Features

* Create a serverless database of user for your web & mobile apps.
  * What does "serverless database" means in this context?
  * That means that users can use simple login (username and password) to connect into the application.
  * Fetures:
    * Simple login
    * Password rest
    * email & phone verification
    * mfa
    * Federated identities: users from facebook, google, SAML...

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

#### Cognito User Pools (CUP) - Integrations

API Gateway - Authentication

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>
