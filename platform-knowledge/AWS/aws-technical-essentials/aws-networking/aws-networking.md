# Introduction to Networking

> **Networking is how you connect computers around the world and allow them to communicate with one another.**
> 
- AWS creates a VPC for each instances with the default option, when a custom VPC config isn’t available

### **Networking defined**

Networking is how you connect computers around the world and allow them to communicate with one another. In this course, you’ve already seen a few examples of networking. One is the AWS Global Infrastructure. AWS has built a network of resources using data centers, Availability Zones, and Regions.

### **Networking basics**

One way to think about networking is to think about sending a letter. When you send a letter, you provide the following three elements:

- The letter, inside the envelope
- The address of the sender in the *from* section
- The address of the recipient in the *to* section

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1713787200/jjVus1M48g1OWJ6r7uenJw/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/vJl58GZqEGnn-ZMs_rgpc8fwnCRi_VmsQ.png

Each address must contain specific information:

- Name of sender or recipient
- Street
- City
- State or province
- Zip, area, or postal code
- Country

You need all parts of an address to ensure that your letter gets to its destination. Without the correct address, postal workers cannot properly deliver the letter. In the digital world, computers handle the delivery of messages in a similar way. This is called routing.

## **IP addresses**

To properly route your messages to a location, you need an address. Just like each home has a mailing address, each computer has an IP address. However, instead of using the combination of street, city, state, zip code, and country, the IP address uses a combination of bits, 0s and 1s.

Here is an example of a 32-bit address in binary format:

A 32-bit address written in binary format.

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1713787200/jjVus1M48g1OWJ6r7uenJw/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/kh6j-7gjj-kFY_hB_MqSUJDRMLwF_EJf5.png

It’s called 32 bit because you have 32 digits. Feel free to count!

## **IPv4 notation**

Typically, you don’t see an IP address in its binary format. Instead, it’s converted into decimal format and noted as an IPv4 address.

In the following diagram, the 32 bits are grouped into groups of 8 bits, also called octets. Each of these groups is converted into decimal format separated by a period.

An IPv4 address, for example, 192.168.1.30 is converted from four groups of eight bits.

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1713787200/jjVus1M48g1OWJ6r7uenJw/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/0YtHqGjwtINbCMjP_3O1LCsMztT9hP6Gv.png

In the end, this is what is called an IPv4 address. This is important to know when trying to communicate to a single computer. But remember, you’re working with a network. This is where Classless Inter-Domain Routing (CIDR) comes in.

## **CIDR notation**

192.168.1.30 is a single IP address. If you want to express IP addresses between the range of 192.168.1.0 and 192.168.1.255, how can you do that?

One way is to use CIDR notation. CIDR notation is a compressed way of representing a range of IP addresses. Specifying a range determines how many IP addresses are available to you.

CIDR notation is shown here.

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1713787200/jjVus1M48g1OWJ6r7uenJw/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/Pjs0q13feA_j6wDK_spqIyeTVAORW0ECH.png

It begins with a starting IP address and is separated by a forward slash (the */* character) followed by a number. The number at the end specifies how many of the bits of the IP address are fixed. In this example, the first 24 bits of the IP address are fixed. The rest (the last 8 bits) are flexible.

!https://explore.skillbuilder.aws/files/a/w/aws_prod1_docebosaas_com/1713787200/jjVus1M48g1OWJ6r7uenJw/tincan/7b5246b3e4dcf41ee9510fd1863163b18f6b0358/assets/fVG7KtazO3_zpy0u_gmxwVotClkzU1FdE.png

32 total bits subtracted by 24 fixed bits leaves 8 flexible bits. Each of these flexible bits can be either 0 or 1, because they are binary. That means that you have two choices for each of the 8 bits, providing 256 IP addresses in that IP range.

The higher the number after the /, the smaller the number of IP addresses in your network. For example, a range of 192.168.1.0/24 is smaller than 192.168.1.0/16.

When working with networks in the AWS Cloud, you choose your network size by using CIDR notation. In AWS, the smallest IP range you can have is /28, which provides 16 IP addresses. The largest IP range you can have is a /16, which provides 65,536 IP addresses.

## **Resources**

[(opens in a new tab)](https://web.stanford.edu/class/cs101/network-1-introduction.html)For more information, see the following resources:

- External website: [Stanford: Introduction to Computer Networking(opens in a new tab)](https://web.stanford.edu/class/cs101/network-1-introduction.html)
- AWS user guide: [How Amazon VPC Works(opens in a new tab)](https://docs.aws.amazon.com/vpc/latest/userguide/how-it-works.html)
- External website: [Wikipedia: Classless Inter-Domain Routing(opens in a new tab)](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing)
- External website: [CIDR.xyz: An interactive IP Address and CIDR Range Visualizer](https://cidr.xyz/)