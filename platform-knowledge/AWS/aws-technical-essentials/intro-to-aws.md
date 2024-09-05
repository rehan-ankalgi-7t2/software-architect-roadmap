# Intro to AWS

[View on Eraser![AWS Basic Architecture](https://app.eraser.io/workspace/uMwP1mmls5FNoFXKOTSL/preview?elements=MRimU0JpImBZlXdCvEFYaw&type=embed)](https://app.eraser.io/workspace/uMwP1mmls5FNoFXKOTSL?elements=MRimU0JpImBZlXdCvEFYaw)

### Ways to interact with AWS services

- AWS Management console
- AWS cli
- AWS Sdk

### AWS region considerations

- Compliance
- Latency
- Pricing
- Service availability

## Security and The AWS shared responsibility model
| Role | Responsibilities |
| --- | --- |
| Cutomers | Cutomer Data, Platform Applications, IAM, OS, Firewall, network config, client-side data encryption, server-side encryption, Network Traffic protection |
| AWS | Software, Storage, Compute, Database, Networking, Hardware (AWS Global infra), Regions, AZs, Edge Location |

### AWS responsibility

| **Category** | **Examples of AWS Services in the Category** | **AWS Responsibility** |
| --- | --- | --- |
| Infrastructure services | Compute services, such as Amazon Elastic Compute Cloud (Amazon EC2) | AWS manages the underlying infrastructure and foundation services. |
| Container services | Services that require less management from the customer, such as Amazon Relational Database Service (Amazon RDS) | AWS manages the underlying infrastructure and foundation services, operating system, and application platform. |
| Abstracted services | Services that require very little management from the customer, such as Amazon Simple Storage Service (Amazon S3) | AWS operates the infrastructure layer, operating system, and platforms, in addition to server-side encryption and data protection. |

### Customer responsibilty

| **Category** | **AWS Responsibility** | **Customer Responsibility** |
| --- | --- | --- |
| Infrastructure services | AWS manages the infrastructure and foundation services. | You control the operating system and application platform, in addition to encrypting, protecting, and managing customer data. |
| Container services | AWS manages the infrastructure and foundation services, operating system, and application platform. | You are responsible for customer data, encrypting the data, and protecting it through network firewalls and backups. |
| Abstracted services | AWS operates the infrastructure layer, operating system, and platforms, in addition to server-side encryption and data protection. | You are responsible for managing customer data and protecting it through client-side encryption. |

## AWS Identity and Access Management

AWS Identity and Access Management (IAM) is an AWS service that helps you manage access to your AWS account and resources. It also provides a centralized view of who and what are allowed inside your AWS account (authentication), and who and what have permissions to use and work with your AWS resources (authorization).

### **IAM features**

To help control access and manage identities in your AWS account, IAM offers many features to ensure security.

- IAM is global and not specific to any one Region. You can see and use your IAM configurations from any Region in the AWS Management Console.
- IAM is integrated with many AWS services by default.
- You can establish password policies in IAM to specify complexity requirements and mandatory rotation periods for users.
- IAM supports MFA.
- IAM supports identity federation, which allows users who already have passwords elsewhere – for example, in your corporate network or with an internet identity provider – to get temporary access to your AWS account.
- Any AWS customer can use IAM; the service is offered at no additional charge.

### **IAM user credentials**

An IAM user consists of a name and a set of credentials. When you create a user, you can provide them with the following types of access:

- Access to the AWS Management Console
- Programmatic access to the AWS Command Line Interface (AWS CLI) and AWS application programming interface (AWS API)

### **IAM groups**

An IAM group is a collection of users. All users in the group inherit the permissions assigned to the group. This makes it possible to give permissions to multiple users at once. It’s a more convenient and scalable way of managing permissions for users in your AWS account. This is why using IAM groups is a best practice.

### **IAM policies**

To manage access and provide permissions to AWS services and resources, you create IAM policies and attach them to IAM users, groups, and roles. Whenever a user or role makes a request, AWS evaluates the policies associated with them. For example, if you have a developer inside the developers group who makes a request to an AWS service, AWS evaluates any policies attached to the developers group and any policies attached to the developer user to determine if the request should be allowed or denied.

### **IAM policy examples**

Most policies are stored in AWS as JSON documents with several policy elements. The following example provides admin access through an IAM identity-based policy.

```json
{
	"Version": "2012-10-17",
	"Statement": [{
		"Effect": "Allow",
		"Action": "*",
		"Resource": "*"
	}]
}
```

---

This policy has four major JSON elements: ***Version***, ***Effect***, ***Action***, and ***Resource***.

- The ***Version*** element defines the version of the policy language. It specifies the language syntax rules that are needed by AWS to process a policy. To use all the available policy features, include **"Version": "2012-10-17"** before the **"Statement"** element in your policies.
- The ***Effect*** element specifies whether the statement will allow or deny access. In this policy, the Effect is **"Allow"**, which means you’re providing access to a particular resource.
- The ***Action*** element describes the type of action that should be allowed or denied. In the example policy, the action is **"*"**. This is called a wildcard, and it is used to symbolize every action inside your AWS account.
- The ***Resource*** element specifies the object or objects that the policy statement covers. In the policy example, the resource is the wildcard **"*"**. This represents all resources inside your AWS console.

Putting this information together, you have a policy that allows you to perform all actions on all resources in your AWS account. This is what we refer to as an administrator policy.The next example shows a more granular IAM policy.

```json
{
	"Version": "2012-10-17",
	"Statement": [{
		"Effect": "Allow",
		"Action": [
			"iam: ChangePassword",
			"iam: GetUser"
		]
		"Resource": "arn:aws:iam::123456789012:user/${aws:username}"
		}]
}
```

---

After looking at the JSON, you can see that this policy allows the IAM user to change their own IAM password (***iam:ChangePassword***) and get information about their own user (***iam:GetUser***). It only permits the user to access their own credentials because the resource restricts access with the variable substitution ***${aws:username}***.

### **Policy structure**

When creating a policy, each of the elements shown in the table are required in the policy statement.

| **Element** | **Description** | **Required** | **Example** |
| --- | --- | --- | --- |
| ***Effect*** | Specifies whether the statement results in an allow or an explicit deny | **√** | ***"Effect": "Deny"*** |
| ***Action*** | Describes the specific actions that will be allowed or denied | **√** | ***"Action": "iam:CreateUser"*** |
| ***Resource*** | Specifies the object or objects that the statement covers | **√** | ***"Resource": "arn:aws:iam::account-ID-without-hyphens:user/Bob"*** |

## Role based access

### IAM best practices

- **Lock down the AWS root user**
    
    The root user is an all-powerful and all-knowing identity in your AWS account. If a malicious user were to gain control of root-user credentials, they would be able to access every resource in your account, including personal and billing information. To lock down the root user, you can do the following:
    
    - Don’t share the credentials associated with the root user
    - Consider deleting the root user access keys
    - Enable MFA on the root account
- **Follow the principle of least privilege**
    
    Least privilege is a standard security principle that advises you to grant only the necessary permissions to do a particular job and nothing more. To implement least privilege for access control, start with the minimum set of permissions in an IAM policy and then grant additional permissions as necessary for a user, group, or role.
    
- **Use IAM appropriately**
    
    IAM is used to secure access to your AWS account and resources. It simply provides a way to create and manage users, groups, and roles to access resources in a single AWS account. IAM is not used for website authentication and authorization, such as providing users of a website with sign-in and sign-up functionality. IAM also does not support security controls for protecting operating systems and networks.
    
- **Use IAM roles when possible**
    
    Maintaining roles is more efficient than maintaining users. When you assume a role, IAM dynamically provides temporary credentials that expire after a defined period of time, between 15 minutes and 36 hours. Users, on the other hand, have long-term credentials in the form of user name and password combinations or a set of access keys.User access keys only expire when you or the account admin rotates the keys. User login credentials expire if you applied a password policy to your account that forces users to rotate
    
- **Consider using an identity provider**
    
    If you decide to make your cat photo application into a business and begin to have more than a handful of people working on it, consider managing employee identity information through an identity provider (IdP). Using an IdP, whether it's an AWS service such as AWS Single Sign-On or a third-party identity provider, provides a single source of truth for all identities in your organization.You no longer have to create separate IAM users in AWS. You can instead use IAM roles to provide permissions to identities that are federated from your IdP. For example, you have an employee, Martha, who has access to multiple AWS accounts. Instead of creating and managing multiple IAM users named Martha in each of those AWS accounts, you could manage Martha in your company’s IdP. If Martha moves in the company or leaves the company, Martha can be updated in the IdP, rather than in every AWS account in the company.
    
- **Consider AWS Single Sign-On**
    
    If you have an organization that spans many employees and multiple AWS accounts, you might want your employees to sign in with a single credential.AWS SSO is an IdP that lets your users sign in to a user portal with a single set of credentials. It then provides users access to their assigned accounts and applications in a central location.Similar to IAM. AWS SSO offers a directory where you can create users, organize them in groups, set permissions across the groups, and grant access to AWS resources. However, AWS SSO has some advantages over IAM. For example, if you’re using a third-party IdP, you can sync your users and groups to AWS SSO. This removes the burden of having to re-create users that already exist elsewhere, and it enables you to manage the users from your IdP. More importantly, AWS SSO separates the duties between your IdP and AWS, ensuring that your cloud access management is not inside or dependent on your IdP.