# Core Architecture

## Exercise - Explore the Learn sandbox

> Activate the Learn Sandbox
If you haven’t already, use the Activate sandbox button above to activate the Learn sandbox.
If you receive a notice saying Microsoft Learn needs your permission to create Azure resource, use the Review permission button to review and accept the permissions. Once you approve the permissions, it may take a few minutes for the sandbox to activate.

### Tasks for the sandbox

1. **Use the PowerShell CLI**
- Use the PowerShell Get-date command to get the current date and time.
```PowerShell
Get-date
```

Most Azure specific commands will start with the letters az. The Get-date command you just ran is a PowerShell specific command. Let's try an Azure command to check what version of the CLI you're using right now.
```PowerShell
az version

output:
{                                                                             
  "azure-cli": "2.65.0",
  "azure-cli-core": "2.65.0",
  "azure-cli-telemetry": "1.1.0",
  "extensions": {
    "ai-examples": "0.2.5",
    "ml": "2.30.1",
    "ssh": "2.0.5"
  }
}
```

2. **Use the Bash CLI**
- If you’re more familiar with BASH, you can use BASH command instead by shifting to the BASH CLI.
Enter `bash` to switch to the BASH CLI.

```PowerShell
bash
```

3. Use Azure CLI interactive mode
Another way to interact is using the Azure CLI interactive mode. This changes CLI behavior to more closely resemble an integrated development environment (IDE). Interactive mode provides autocompletion, command descriptions, and even examples. If you’re unfamiliar with BASH and PowerShell, but want to use the command line, interactive mode may help you.

Enter az interactive to enter interactive mode.
```Bash
az interactive
```

Decide whether you wish to send telemetry data and enter YES or NO.

You may have to wait a minute or two to allow the interactive mode to fully initialize. Then, enter the letter “a” and auto-completion should start to work. If auto-completion isn’t working, erase what you’ve entered, wait a bit longer, and try again.
![](https://learn.microsoft.com/en-us/training/wwl-azure/describe-core-architectural-components-of-azure/media/azure-interactive-mode-c8421a2d-3c3d662b.png)

4. Use the azure portal
You’ll also have the option of using the Azure portal during sandbox exercises. You need to use the link provided in the exercise to access the Azure portal. Using the provided link, instead of opening the portal yourself, ensures the correct subscription is used and the exercise remains free for you to complete.

Sign in to the Azure portal to check out the Azure web interface. Once in the portal, you can see all the services Azure has to offer as well as look around at resource groups and so on.

## Physical Infrastructure
> **Data Centers**: the datacenters are the same as large corporate datacenters. They’re facilities with resources arranged in racks, with dedicated power, cooling, and networking infrastructure.

Datacenters are grouped into `Azure Regions` or `Azure Availability Zones` that are designed to help you achieve resiliency and reliability for your business-critical workloads.

> A `region` is a geographical area on the planet that contains at least one, but potentially multiple datacenters that are nearby and networked together with a low-latency network. Azure intelligently assigns and controls the resources within each region to ensure workloads are appropriately balanced.

> `Availability zones` are physically separate datacenters within an Azure region.

Each availability zone is made up of one or more datacenters equipped with independent power, cooling, and networking. An availability zone is set up to be an isolation boundary. If one zone goes down, the other continues working. Availability zones are connected through high-speed, private fiber-optic networks.

![](https://learn.microsoft.com/en-us/training/wwl-azure/describe-core-architectural-components-of-azure/media/availability-zones-c22f95a3-14cd8677.png)

Availability zones are primarily for VMs, managed disks, load balancers, and SQL databases. Azure services that support availability zones fall into three categories:

1. Zonal services: You pin the resource to a specific zone (for example, VMs, managed disks, IP addresses).
2. Zone-redundant services: The platform replicates automatically across zones (for example, zone-redundant storage, SQL Database).
3. Non-regional services: Services are always available from Azure geographies and are resilient to zone-wide outages as well as region-wide outages.

### Region Pairs
Most Azure regions are paired with another region within the same geography (such as US, Europe, or Asia) at least 300 miles away. This approach allows for the replication of resources across a geography that helps reduce the likelihood of interruptions because of events such as natural disasters, civil unrest, power outages, or physical network outages that affect an entire region. For example, if a region in a pair was affected by a natural disaster, services would automatically fail over to the other region in its region pair.
Examples of region pairs in Azure are West US paired with East US and South-East Asia paired with East Asia

![](https://learn.microsoft.com/en-us/training/wwl-azure/describe-core-architectural-components-of-azure/media/region-pairs-7c495a33-85c0fa20.png)

### Sovereign Regions
In addition to regular regions, Azure also has sovereign regions. Sovereign regions are instances of Azure that are isolated from the main instance of Azure. You may need to use a sovereign region for compliance or legal purposes.

Azure sovereign regions include:
- US DoD Central, US Gov Virginia, US Gov Iowa and more: These regions are physical and logical network-isolated instances of Azure for U.S. government agencies and partners. These datacenters are operated by screened U.S. personnel and include additional compliance certifications.
- China East, China North, and more: These regions are available through a unique partnership between Microsoft and 21Vianet, whereby Microsoft doesn't directly maintain the datacenters.
