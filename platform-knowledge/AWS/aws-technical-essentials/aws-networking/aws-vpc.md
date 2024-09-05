# Amazon VPC

> A virtual private cloud (VPC) is an isolated network that you create in the AWS Cloud, similar to a traditional network in a data center.
> 

When you create an Amazon VPC, you must choose three main factors:

- Name of the VPC
- Region where the VPC will live – A VPC spans all the Availability Zones within the selected Region.
- IP range for the VPC in CIDR notation – This determines the size of your network. Each VPC can have up to five CIDRs: one primary and four secondaries for IPv4. Each of these ranges can be between /28 (in CIDR notation) and /16 in size.

Using this information, AWS will provision a network and IP addresses for that network.

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1713787200/jjVus1M48g1OWJ6r7uenJw/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/t39keaPeCKlHVRKP_KKtsB2WCJm3nf8cP.png

## **Creating a subnet**

After you create your VPC, you must create subnets inside the network. Think of subnets as smaller networks inside your base network, or virtual local area networks (VLANs) in a traditional, on-premises network. In an on-premises network, the typical use case for subnets is to isolate or optimize network traffic. In AWS, subnets are used to provide high availability and connectivity options for your resources. Use a public subnet for resources that must be connected to the internet and a private subnet for resources that won't be connected to the internet.

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1713787200/jjVus1M48g1OWJ6r7uenJw/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/T9GKeeYk2PJpXmoA_jUajvREe6Ry6idlJ.png

When you create a subnet, you must specify the following:

- **VPC** that you want your subnet to live in—in this case: VPC (10.0.0.0/16)
- **Availability Zone** that you want your subnet to live in—in this case: Availability Zone 1
- **IPv4 CIDR block for your subnet**, which must be a subset of the VPC CIDR block—in this case: 10.0.0.0/24

When you launch an EC2 instance, you launch it inside a subnet, which will be located inside the Availability Zone that you choose.

## **High availability with a VPC**

When you create your subnets, keep high availability in mind. To maintain redundancy and fault tolerance, create at least two subnets configured in two Availability Zones.

As you learned earlier, remember that “everything fails all of the time.” With the example network, if one of the Availability Zones fails, you will still have your resources available in another Availability Zone as backup.

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1713787200/jjVus1M48g1OWJ6r7uenJw/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/zFbgStDJuiU7O9Qe_OaaDyPzF7zr1lKW9.png

- Reserved IP
    
    ### **Reserved IPs**
    
    For AWS to configure your VPC appropriately, AWS reserves five IP addresses in each subnet. These IP addresses are used for routing, Domain Name System (DNS), and network management.
    
    For example, consider a VPC with the IP range 10.0.0.0/22. The VPC includes 1,024 total IP addresses. This is then divided into four equal-sized subnets, each with a /24 IP range with 256 IP addresses. Out of each of those IP ranges, there are only 251 IP addresses that can be used because AWS reserves five.
    
    !https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1713787200/jjVus1M48g1OWJ6r7uenJw/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/yVvxJRoMUxkJyMC6_Octk-lV6RnrruL3M.png
    
    The five reserved IP addresses can impact how you design your network. A common starting place for those who are new to the cloud is to create a VPC with an IP range of /16 and create subnets with an IP range of /24. This provides a large amount of IP addresses to work with at both the VPC and subnet levels.

## **Gateways**

### **Internet gateway**

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1713787200/jjVus1M48g1OWJ6r7uenJw/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/ecqwO5Wcc7K4fgNt_cdDgG30XUESG1bod.png

To activate internet connectivity for your VPC, you must create an internet gateway. Think of the gateway as similar to a modem. Just as a modem connects your computer to the internet, the internet gateway connects your VPC to the internet. Unlike your modem at home, which sometimes goes down or offline, an internet gateway is highly available and scalable. After you create an internet gateway, you attach it to your VPC.

### **Virtual private gateway**

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1713787200/jjVus1M48g1OWJ6r7uenJw/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/UgK7Zqk8CjPnR5H1_eB71WD-OxzwmjLTG.jpg

A virtual private gateway connects your VPC to another private network. When you create and attach a virtual private gateway to a VPC, the gateway acts as anchor on the AWS side of the connection. On the other side of the connection, you will need to connect a customer gateway to the other private network. A customer gateway device is a physical device or software application on your side of the connection. When you have both gateways, you can then establish an encrypted virtual private network (VPN) connection between the two sides.

- AWS Direct Connect
    
    #### **AWS Direct Connect**
    
    To establish a secure physical connection between your on-premises data center and your Amazon VPC, you can use AWS Direct Connect. With AWS Direct Connect, your internal network is linked to an AWS Direct Connect location over a standard Ethernet fiber-optic cable. This connection allows you to create virtual interfaces directly to public AWS services or to your VPC.
    
    !https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1713787200/jjVus1M48g1OWJ6r7uenJw/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/lfpQ8pS_WPGFX2v-_CC16Zxyi_ii4JBzG.png
    

## **Resources**

For more information, see the following resources:

[(opens in a new tab)](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Scenario2.html)[(opens in a new tab)](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html)

- AWS user guide: [What Is Amazon VPC?(opens in a new tab)](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html)
- AWS user guide: [How Amazon VPC Works(opens in a new tab)](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html)
- AWS user guide: [How AWS Site-to-Site VPN Works(opens in a new tab)](https://docs.aws.amazon.com/vpn/latest/s2svpn/how_it_works.html)[(opens in a new tab)](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html)
- AWS user guide: [What Is AWS Direct Connect(opens in a new tab)](https://docs.aws.amazon.com/directconnect/latest/UserGuide/Welcome.html)?