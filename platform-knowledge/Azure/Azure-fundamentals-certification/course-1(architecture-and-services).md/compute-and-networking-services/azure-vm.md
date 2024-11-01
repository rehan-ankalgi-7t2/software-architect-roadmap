# Azure Virtual Machines

- VMs provide infrastructure as a service (IaaS) in the form of a virtualized server and can be used in many ways. 

- Just like a physical computer, you can customize all of the software running on your VM. VMs are an ideal choice when you need:
    - Total control over the operating system (OS).
    - The ability to run custom software.
    - To use custom hosting configurations.

- You can run single VMs for testing, development, or minor tasks. Or you can group VMs together to provide high availability, scalability, and redundancy. 
- Azure can also manage the grouping of VMs for you with features such as `scale sets` and `availability sets`.

### Virtual Machine Scale sets
> Virtual machine scale sets let you create and manage a group of identical, load-balanced VMs

<div style="background-color: #f003; padding: 8px;">
<h4>❗Problem </h4>
If you simply created multiple VMs with the same purpose, you’d need to ensure they were all configured identically and then set up network routing parameters to ensure efficiency. You’d also have to monitor the utilization to determine if you need to increase or decrease the number of VMs.
</div>

- with virtual machine scale sets, Azure automates most of that work. Scale sets allow you to centrally manage, configure, and update a large number of VMs in minutes. 
- The number of VM instances can automatically increase or decrease in response to demand, or you can set it to scale based on a defined schedule. 
- Virtual machine scale sets also automatically deploy a load balancer to make sure that your resources are being used efficiently. 
- With virtual machine scale sets, you can build large-scale services for areas such as compute, big data, and container workloads.

### Virtual Machine Availability Sets
Virtual machine availability sets are another tool to help you build a more resilient, highly available environment. Availability sets are designed to ensure that VMs stagger updates and have varied power and network connectivity, preventing you from losing all your VMs with a single network or power failure.

Availability accomplish these objectives by grouping VMs in two ways: update domain and fault domain.

- **Update domain**: The update domain groups VMs that can be rebooted at the same time. This setup allows you to apply updates while knowing that only one update domain grouping is offline at a time. All of the machines in one update domain update. An update group going through the update process is given a 30-minute time to recover before maintenance on the next update domain starts.
- **Fault domain**: The fault domain groups your VMs by common power source and network switch. By default, an availability set splits your VMs across up to three fault domains. This helps protect against a physical power or networking failure by having VMs in different fault domains (thus being connected to different power and networking resources).

> 👍 Best of all, there’s no additional cost for configuring an availability set. You only pay for the VM instances you create.

Some common examples or use cases for virtual machines include:

- During testing and development.
- When running applications in the cloud.
- When extending your datacenter to the cloud
- During disaster recovery

### VM Resources
When you provision a VM, you’ll also have the chance to pick the resources that are associated with that VM, including:

- Size (purpose, number of processor cores, and amount of RAM)
- Storage disks (hard disk drives, solid state drives, etc.)
- Networking (virtual network, public IP address, and port configuration)
