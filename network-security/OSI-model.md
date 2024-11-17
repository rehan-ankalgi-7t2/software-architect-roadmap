# OSI Model

 > the OSI provides a standard for different computer systems to be able to communicate with each other.

The OSI Model can be seen as a universal language for computer networking. It is based on the concept of splitting up a communication system into seven abstract layers, each one stacked upon the last.


![](https://cf-assets.www.cloudflare.com/slt3lc6tev37/6ZH2Etm3LlFHTgmkjLmkxp/59ff240fb3ebdc7794ffaa6e1d69b7c2/osi_model_7_layers.png)

### Why does OSI Layer model matter?
Although the modern Internet does not strictly follow the OSI Model (it more closely follows the simpler Internet protocol suite), the OSI Model is still very useful for troubleshooting network problems. Whether it’s one person who can’t get their laptop on the Internet, or a website being down for thousands of users, the OSI Model can help to break down the problem and isolate the source of the trouble. If the problem can be narrowed down to one specific layer of the model, a lot of unnecessary work can be avoided.

## 7. Application Layer
![](https://cf-assets.www.cloudflare.com/slt3lc6tev37/2rcDKpr4WLqoyAZ7GDKkyJ/7cab96402de7ac5465b86e617da3da4e/osi_model_application_layer_7.png)

- Software applications like web browsers and email clients rely on the application layer to initiate communications.
- client software applications are not part of the application layer; rather the application layer is responsible for the protocols and data manipulation that the software relies on to present meaningful data to the user.
- Application layer protocols include HTTP as well as SMTP

## 6. Presentation Layer
![](https://cf-assets.www.cloudflare.com/slt3lc6tev37/19L86neKKT8srUkOSe4rf7/ff4c91c94a1790651df7b48433913f59/osi_model_presentation_layer_6.png)

- makes the data presentable for applications to consume.
- The presentation layer is responsible for translation, encryption, and compression of data.
- the presentation layer is also responsible for compressing data it receives from the application layer before delivering it to layer 5. This helps improve the speed and efficiency of communication by minimizing the amount of data that will be transferred.

## 5. Session Layer
![](https://cf-assets.www.cloudflare.com/slt3lc6tev37/29mRrgK22AqJVlg2MMlD86/34d8f4071b6cc0d3b03c93f55e4d89b7/osi_model_session_layer_5.png)

- the layer responsible for opening and closing communication between the two devices.
- The time between when the communication is opened and closed is known as the session.
- The session layer ensures that the session stays open long enough to transfer all the data being exchanged, and then promptly closes the session in order to avoid wasting resources.

- The session layer also synchronizes data transfer with checkpoints.   

    **For example**, if a 100 megabyte file is being transferred, the session layer could set a checkpoint every 5 megabytes. In the case of a disconnect or a crash after 52 megabytes have been transferred, the session could be resumed from the last checkpoint, meaning only 50 more megabytes of data need to be transferred. Without the checkpoints, the entire transfer would have to begin again from scratch.

## 4. Transport Layer
![](https://cf-assets.www.cloudflare.com/slt3lc6tev37/3OlO75NcADGL3SmEADFDqd/723b8c7639c4e2e6b4febcbe7fd36e0e/osi_model_transport_layer_4.png)

- Layer 4 is responsible for end-to-end communication between the two devices. 
- This includes taking data from the session layer and breaking it up into chunks called segments before sending it to layer 3. 
- The transport layer on the receiving device is responsible for reassembling the segments into data the session layer can consume.

- The transport layer is also responsible for `flow control` and `error control`. 
    - `Flow control` determines an optimal speed of transmission to ensure that a sender with a fast connection does not overwhelm a receiver with a slow connection. 
    
    - The transport layer performs `error control` on the receiving end by ensuring that the data received is complete, and requesting a retransmission if it isn’t.

- Transport layer protocols include the `Transmission Control Protocol (TCP)` and the `User Datagram Protocol (UDP)`.


## 3. Network Layer
![](https://cf-assets.www.cloudflare.com/slt3lc6tev37/3g2Hv0frHsql5SFauJL5EG/d8cede7b6a780e63413bd86de9eee7f9/osi_model_network_layer_3.png)

> The network layer is responsible for facilitating data transfer between two different networks. 

- If the two devices communicating are on the same network, then the network layer is unnecessary.

- The network layer breaks up segments from the transport layer into smaller units, called `packets`, on the sender’s device, and reassembling these packets on the receiving device. 
- The network layer also finds the best physical path for the data to reach its destination; this is known as `routing`.

Network layer protocols include `IP`, the `Internet Control Message Protocol (ICMP)`, the `Internet Group Message Protocol (IGMP)`, and the `IPsec suite`.

## 2. Data Link Layer
![](https://cf-assets.www.cloudflare.com/slt3lc6tev37/3TLHavXiotb9ayyZFKECf3/9456d1c431cd71ceea7f4b407f076f11/data_link_layer_osi_model.png)

> the data link layer facilitates data transfer between two devices on the same network. 

- The data link layer takes packets from the network layer and breaks them into smaller pieces called `frames`. 
- Like the transport layer, the data link layer is also responsible for `flow control` and `error control` in `intra-network communication` (The transport layer only does flow control and error control for inter-network communications).


## 1. Physical Layer
![](https://cf-assets.www.cloudflare.com/slt3lc6tev37/1HQ1W5P4XAinIdM37DTu4U/900ccdceda346baf03ce8b9f977d2974/osi_model_physical_layer_1.png)

- This layer includes the physical equipment involved in the data transfer, such as the cables and switches. 
- This is also the layer where the data gets converted into a bit stream, which is a string of 1s and 0s. 
- The physical layer of both devices must also agree on a signal convention so that the 1s can be distinguished from the 0s on both devices.
