# Serverless with AWS Fargate

Is there a way to remove some of this undifferentiated heavy lifting? Yes! If you want to deploy your workloads and applications without having to manage any EC2 instances, you can do that on AWS with serverless compute.
With serverless compute, you can spend time on the things that differentiate your application, rather than spending time on ensuring availability, scaling, and managing servers. Every definition of serverless mentions the following four aspects:

- There are no servers to provision or manage.
- It scales with usage.
- You never pay for idle resources.
- Availability and fault tolerance are built in.

AWS has developed serverless services for all three layers of the application stack. We will cover two services, AWS Fargate and AWS Lambda, in the following lessons.

## Resources

[(opens in a new tab)](https://aws.amazon.com/serverless/#:~:text=Serverless%20is%20the%20native%20architecture,services%20without%20thinking%20about%20servers.)For more information, see the following resources:

- AWS website: [Serverless on AWS(opens in a new tab)](https://aws.amazon.com/serverless/#:~:text=Serverless%20is%20the%20native%20architecture,services%20without%20thinking%20about%20servers.)
- AWS website: [AWS Serverless Resources](https://aws.amazon.com/serverless/resources/?serverless.sort-by=item.additionalFields.createdDate&serverless.sort-order=desc)

> **AWS Fargate scales and manages the infrastructure, so developers can work on what they do best, application development.**
> 

Fargate abstracts the EC2 instance so that you’re not required to manage the underlying compute infrastructure. However, with Fargate, you can use all the same Amazon ECS concepts, APIs, and AWS integrations. It natively integrates with IAM and Amazon Virtual Private Cloud (Amazon VPC). With native integration with Amazon VPC, you can launch Fargate containers inside your network and control connectivity to your applications.

AWS Fargate

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1713787200/jjVus1M48g1OWJ6r7uenJw/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/7tDhRKokT_V2-RiI__waFpJh3C3F9hik_.jpg

AWS Fargate is a purpose-built serverless compute engine for containers. AWS Fargate scales and manages the infrastructure, so developers can work on what they do best, application development. It achieves this by allocating the right amount of compute. This eliminates the need to choose and manage EC2 instances, cluster capacity, and scaling. Fargate supports both Amazon ECS and Amazon EKS architecture and provides workload isolation and improved security by design.

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1713787200/jjVus1M48g1OWJ6r7uenJw/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/8p5CW5OjoI1_2ybG_sged-PS8V6WKvnHk.jpg