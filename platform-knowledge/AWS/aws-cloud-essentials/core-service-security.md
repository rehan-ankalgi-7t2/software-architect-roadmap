# Core service `Security`
## The Shared Responsibility Model

This model describes specifically what the customers and AWS are responsible for maintaining. It is also important to get used to terminology used in the Shared Responsibility Model.

<aside>
💡 **AWS responsibility "Security of the Cloud":** AWS is responsible for protecting the infrastructure that runs all of the services offered in the AWS Cloud. This infrastructure is composed of the hardware, software, networking, and all of the physical and environmental controls that run AWS Cloud services.

**Customer** **responsibility "Security in the Cloud":** Customer responsibility will be determined by the AWS Cloud services that a customer selects.

</aside>

### Customer Responsibilities

- Platform, applications, and identity and access management
- Operating system, network, and firewall configuration
- Client-side data encryption and data integrity authentication
- Server-side encryption (File system and data)
- Network traffic protection (Encryption, integrity, and identity)

### AWS responsibilities: Security of the cloud

AWS is responsible for protecting the infrastructure that runs all of the services offered in the AWS Cloud. This infrastructure comprises the hardware, software, networking, and facilities that run AWS Cloud services.

- **AWS software (**Compute, Storage, Databases, Networking)
- **Hardware and AWS Global Infrastructure (**Regions, Availability Zones, and Edge Locations)

## AWS Compliance

AWS Security Services

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/499e7616-60bf-4e7f-94b9-9a2c79c5f331/Untitled.png)

**IAM**

AWS Identity and Access Management (IAM) is one of the first services you learn about because this service helps you control access to your AWS resources.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c51246c3-606c-4921-97cc-df01fc9049f2/Untitled.png)

**AWS Artifact**

Use the AWS Artifact service to generate on-demand compliance reports.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bf460f6d-fa28-4b86-ac05-f66bbb4d5f87/Untitled.png)

**AWS KMS**

AWS Key Management Service (AWS KMS) helps you generate, manage, and rotate your encryption keys. You can also control who has access to those keys.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/49feee1c-31fb-4865-99b3-1081ab3d6a74/Untitled.png)

**AWS Shield**

Shield protects you from common distributed denial of service (DDoS) attacks.

## AWS Trusted Advisor

<aside>
💡 AWS Trusted Advisor guides you on how to reduce cost, increase performance, and improve security.

</aside>

AWS Trusted Advisor provides recommendations that help you follow AWS best practices. Trusted Advisor evaluates your account by using checks. These checks identify ways to optimize your AWS infrastructure, improve security and performance, reduce costs, and monitor service quotas. You can then follow the recommendations to optimize your services and resources.

Trusted Advisor analyzes your environments across five dimensions: cost optimization, performance, security, fault tolerance, and service limits.

To learn about the benefits of Trusted Advisor, flip the following flashcards by choosing them. To move to the previous card, choose the left arrow. To move to the next card, choose the right arrow.