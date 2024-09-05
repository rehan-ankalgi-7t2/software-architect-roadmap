# Container Services 🚢

Although containers are often referred to as a new technology, the idea started in the 1970s with certain UNIX kernels (the central core of the operating system) having the ability to separate their processes through isolation. At the time, this was configured manually, making operations complex.

With the evolution of the open-source software community, containers evolved. Today, containers are used as a solution to problems of traditional compute, including the issue of getting software to run reliably when it moves from one compute environment to another.

<aside>
💡 A container is a standardized unit that packages your code and its dependencies. This package is designed to run reliably on any platform, because the container creates its own independent environment. With containers, workloads can be carried from one place to another, such as from development to production or from on-premises environments to the cloud.

</aside>

An example of a containerization platform is `Docker`. Docker is a popular container runtime that simplifies the management of the entire operating system stack required for container isolation, including networking and storage. Docker helps customers create, package, deploy, and run containers.

## difference between VMs and containers

![Screenshot 2024-04-22 at 1.23.52 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/89306d87-fba5-419f-8eb3-bf584d2697e3/cbf6f191-621d-4ec8-82fe-cf9fdd3626b4/Screenshot_2024-04-22_at_1.23.52_PM.png)

Containers share the same operating system and kernel as the host that they exist on. But virtual machines contain their own operating system. Each virtual machine must maintain a copy of an operating system, which results in a degree of wasted resources.

A container is more lightweight. Containers spin up quicker, almost instantly. This difference in startup time becomes instrumental when designing applications that must scale quickly during I/O bursts.

Containers can provide speed, but virtual machines offer the full strength of an operating system and more resources, like package installation, dedicated kernel, and more.

## Orchestrating containers

In AWS, containers can run on EC2 instances. For example, you might have a large instance and run a few containers on that instance. Although running one instance is uncomplicated to manage, it lacks high availability and scalability. Most companies and organizations run many containers on many EC2 instances across several Availability Zones.

If you’re trying to manage your compute at a large scale, you should consider the following:

- How to place your containers on your instances
- What happens if your container fails
- What happens if your instance fails
- How to monitor deployments of your containers

This coordination is handled by a container orchestration service. AWS offers two container orchestration services: Amazon Elastic Container Service (Amazon ECS) and Amazon Elastic Kubernetes Service (Amazon EKS).

## Managing containers with `Amazon ECS`

Amazon ECS is an end-to-end container orchestration service that helps you spin up new containers. With Amazon ECS, your containers are defined in a task definition that you use to run an individual task or a task within a service. You have the option to run your tasks and services on a serverless infrastructure that's managed by another AWS service called AWS Fargate. Alternatively, for more control over your infrastructure, you can run your tasks and services on a cluster of EC2 instances that you manage.

![Screenshot 2024-04-22 at 1.28.12 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/89306d87-fba5-419f-8eb3-bf584d2697e3/c3f723be-7502-47a6-abeb-5dc8b713a77e/Screenshot_2024-04-22_at_1.28.12_PM.png)

If you choose to have more control by running and managing your containers on a cluster of Amazon EC2 instances, you will also need to install the Amazon ECS container agent on your EC2 instances. Note that an EC2 instance with the container agent installed is often called a container instance. This container agent is open source and responsible for communicating to the Amazon ECS service about cluster management details. You can run the agent on both Linux and Windows AMIs. 

![Screenshot 2024-04-22 at 1.35.17 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/89306d87-fba5-419f-8eb3-bf584d2697e3/ea5369cd-319b-495a-a884-cd2e13320f66/Screenshot_2024-04-22_at_1.35.17_PM.png)

When the Amazon ECS container instances are up and running, you can perform actions that include, but are not limited to, the following:

- Launching and stopping containers
- Getting cluster state
- Scaling in and out
- Scheduling the placement of containers across your cluster
- Assigning permissions
- Meeting availability requirements

To prepare your application to run on Amazon ECS, you create a task definition. The task definition is a text file, in JSON format, that describes one or more containers. A task definition is similar to a blueprint that describes the resources that you need to run a container, such as CPU, memory, ports, images, storage, and networking information.

Here is a simple task definition that you can use for your corporate directory application. In this example, this runs on the Nginx web server.

```jsx
{
	"family": "webserver",
	"containerDefinitions": [ {
	"name": "web",
	"image": "nginx",
	"memory": "100",
	"cpu": "99"
	} ],
	"requiresCompatibilities": [ "FARGATE" ],
	"networkMode": "awsvpc",
	"memory": "512",
	"cpu": "256"
}
```