# Using Kubernetes with Amazon EKS
<aside>
💡 Kubernetes is a portable, extensible, open-source platform for managing containerized workloads and services.

</aside>
By bringing software development and operations together by design, Kubernetes created a rapidly growing ecosystem that is very popular and well established in the market.

If you already use Kubernetes, you can use Amazon EKS to orchestrate the workloads in the AWS Cloud. Amazon EKS is a managed service that you can use to run Kubernetes on AWS without needing to install, operate, and maintain your own Kubernetes control plane or nodes. Amazon EKS is conceptually similar to Amazon ECS, but with the following differences:

- In Amazon ECS, the machine that runs the containers is an EC2 instance that has an ECS agent installed and configured to run and manage your containers. This instance is called a container instance. In Amazon EKS, the machine that runs the containers is called a worker node or Kubernetes node.
- An ECS container is called a task. An EKS container is called a pod.
- Amazon ECS runs on AWS native technology. Amazon EKS runs on Kubernetes.

If you have containers running on Kubernetes and want an advanced orchestration solution that can provide simplicity, high availability, and fine-grained control over your infrastructure, Amazon EKS could be the tool for you.

# **Resources**

[(opens in a new tab)](https://aws.amazon.com/containers/services/)For more information, see the following resources:

- AWS website: [Containers on AWS(opens in a new tab)](https://aws.amazon.com/containers/services/)
- External website: [Docker: Use Containers to Build, Share and Run Your Applications(opens in a new tab)](https://www.docker.com/resources/what-container)
- AWS website: [Amazon Elastic Container Service (Amazon ECS)(opens in a new tab)](https://aws.amazon.com/ecs/)
- External website: [Github: Amazon ECS Agent(opens in a new tab)](https://github.com/aws/amazon-ecs-agent)
- AWS developer guide: [Amazon ECS Container Instances(opens in a new tab)](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/ECS_instances.html)
- External website: [Coursera course: Building Containerized Applications on AWS(opens in a new tab)](https://www.coursera.org/learn/containerized-apps-on-aws)
- AWS website: [Amazon Elastic Kubernetes Service (EKS)(opens in a new tab)](https://aws.amazon.com/eks/)
- AWS user guide: [Amazon EKS User Guide](https://docs.aws.amazon.com/eks/latest/userguide/what-is-eks.html)