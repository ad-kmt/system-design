# OSI Model

## What is the OSI Model?
The Open Systems Interconnection (OSI) model is a conceptual framework created by the International Organization for Standardization (ISO). It enables diverse communication systems to communicate using standard protocols.

In simple terms, the OSI model provides a universal language for computer networking, allowing different computer systems to interact with each other.

The OSI model splits a communication system into seven abstract layers, each one stacked upon the last. These layers are: physical, data link, network, transport, session, presentation, and application.

## Why does the OSI Model Matter?
Although the modern Internet follows the simpler Internet Protocol Suite rather than the OSI model, the OSI model remains useful for troubleshooting network problems. Whether dealing with individual connectivity issues or large-scale outages, the OSI model helps break down and isolate the source of problems, often saving time and effort by narrowing down the issue to a specific layer.

## The 7 Layers of the OSI Model
Each layer of the OSI model handles a specific job and communicates with the layers directly above and below it. Here’s a detailed look at each layer:

![](https://www.lifewire.com/thmb/li3H7yhEr-D8Vo6MC1Hymi_AvDk=/1500x0/filters:no_upscale():max_bytes(150000):strip_icc()/OSImodel-8d93f19d50e543348f82110aa11f7a93.jpg)

![](https://miro.medium.com/v2/resize:fit:679/1*7yPBGx_K8GymgeGfzhfznA.gif)

### 7. The Application Layer
**Purpose:** This is the only layer that directly interacts with user data. It manages the protocols and data manipulation required by software applications like web browsers and email clients.

**Note**: Client software applications are not part of the application layer; rather the application layer is responsible for the protocols and data manipulation that the software relies on to present meaningful data to the user.

**Protocols:** HTTP, SMTP (Simple Mail Transfer Protocol)

![](https://cf-assets.www.cloudflare.com/slt3lc6tev37/2rcDKpr4WLqoyAZ7GDKkyJ/7cab96402de7ac5465b86e617da3da4e/osi_model_application_layer_7.png)

### 6. The Presentation Layer
**Purpose:** Prepares data for the application layer. It handles translation, encryption, and compression of data.

- **Translation:** Two communicating devices communicating may be using different encoding methods, so layer 6 is responsible for translating incoming data into a syntax that the application layer of the receiving device can understand.
- **Encryption/Decryption:** If the devices are communicating over an encrypted connection, layer 6 is responsible for adding the encryption on the sender’s end as well as decoding the encryption on the receiver's end
- **Compression:** also responsible for compressing data it receives from the application layer before delivering it to layer 5. Improve the speed and efficiency of communication by minimizing the amount of data that will be transferred.

![](https://cf-assets.www.cloudflare.com/slt3lc6tev37/19L86neKKT8srUkOSe4rf7/ff4c91c94a1790651df7b48433913f59/osi_model_presentation_layer_6.png)

### 5. The Session Layer
**Purpose:**
- Responsible for opening and closing communication between the two devices.

- **Session**: The time between when the communication is opened and closed is known as the session.

- Manages sessions of communication between devices, ensuring they stay open long enough to transfer all data and close them when done to conserve resources.

- **Synchronization:** Uses checkpoints to ensure data can be resumed from the last point in case of interruption.

**Example**:
- If a 100 megabyte file is being transferred, the session layer could set a checkpoint every 5 megabytes.
- In the case of a disconnect or a crash after 52 megabytes have been transferred, the session could be resumed from the last checkpoint
- Meaning only 50 more megabytes of data need to be transferred.
- Without the checkpoints, the entire transfer would have to begin again from scratch.

![](https://cf-assets.www.cloudflare.com/slt3lc6tev37/29mRrgK22AqJVlg2MMlD86/34d8f4071b6cc0d3b03c93f55e4d89b7/osi_model_session_layer_5.png)

### 4. The Transport Layer
**Purpose:** Provides end-to-end communication between devices. It segments data for transfer and reassembles it at the destination.

**While sending**: taking data from the session layer and breaking it up into chunks called segments before sending it to layer 3.

**While receiving**: taking segments from Network layer and reassembling the segments into data the session layer can consume.

The transport layer is also responsible for flow control and error control.
- **Flow Control:** Adjusts transmission speed to prevent overload.
- **Error Control:** Ensures complete and accurate data transfer, requesting retransmission if necessary.

**Protocols:** TCP (Transmission Control Protocol), UDP (User Datagram Protocol)

![](https://cf-assets.www.cloudflare.com/slt3lc6tev37/3OlO75NcADGL3SmEADFDqd/723b8c7639c4e2e6b4febcbe7fd36e0e/osi_model_transport_layer_4.png)

### 3. The Network Layer
**Purpose:** Facilitates data transfer between two different networks by routing packets.

- If the two devices communicating are on the same network, then the network layer is unnecessary.

- The network layer breaks up segments from the transport layer into smaller units, called packets, on the sender’s device, and reassembling these packets on the receiving device.

- The network layer also finds the best physical path for the data to reach its destination; this is known as routing.

**Protocols:** IP (Internet Protocol), ICMP (Internet Control Message Protocol), IGMP (Internet Group Management Protocol), IPsec (Internet Protocol Security)

![](https://cf-assets.www.cloudflare.com/slt3lc6tev37/3g2Hv0frHsql5SFauJL5EG/d8cede7b6a780e63413bd86de9eee7f9/osi_model_network_layer_3.png)

### 2. The Data Link Layer
**Purpose:** The data link layer is very similar to the network layer, except the data link layer facilitates data transfer between two devices on the **same network**.

The data link layer takes packets from the network layer and breaks them into smaller pieces called frames.

Like the network layer, the data link layer is also responsible for flow control and error control in intra-network communication (The transport layer only does flow control and error control for inter-network communications).

![](https://cf-assets.www.cloudflare.com/slt3lc6tev37/3TLHavXiotb9ayyZFKECf3/9456d1c431cd71ceea7f4b407f076f11/data_link_layer_osi_model.png)

### 1. The Physical Layer
**Purpose:** Handles the physical aspects of data transmission, such as cables and switches. It converts data into a bit stream (1s and 0s) and transmits it over a physical medium.

![](https://cf-assets.www.cloudflare.com/slt3lc6tev37/1HQ1W5P4XAinIdM37DTu4U/900ccdceda346baf03ce8b9f977d2974/osi_model_physical_layer_1.png)

## How Data Flows Through the OSI Model
Data must travel down the seven layers of the OSI model on the sending device and then up the seven layers on the receiving device. Here’s an example:

**Sending an Email:**
1. **Application Layer:** Mr. Cooper’s email application uses SMTP to send the email.
2. **Presentation Layer:** Data is compressed and encrypted.
3. **Session Layer:** Communication session is initiated.
4. **Transport Layer:** Data is segmented.
5. **Network Layer:** Segments are broken into packets.
6. **Data Link Layer:** Packets are broken into frames.
7. **Physical Layer:** Frames are converted into bitstream and transmitted.

**Receiving the Email:**
1. **Physical Layer:** Bitstream is received and converted into frames.
2. **Data Link Layer:** Frames are reassembled into packets.
3. **Network Layer:** Packets are reassembled into segments.
4. **Transport Layer:** Segments are reassembled into data.
5. **Session Layer:** Communication session is closed.
6. **Presentation Layer:** Data is decompressed and decrypted.
7. **Application Layer:** Data is presented to Ms. Palmer’s email application.

## Related Topics
- **TCP/IP Model:** Understanding the differences and similarities between the OSI and TCP/IP models.
- **Network Protocols:** Deep dive into specific protocols like HTTP, TCP, UDP, and IP.

## Topics for Deeper Understanding
- **Network Troubleshooting:** Techniques and tools for diagnosing network issues using the OSI model.
- **DDoS Attacks:** Understanding how different layers of the OSI model are targeted in DDoS attacks.
- **Data Encryption and Compression:** In-depth study of how data is secured and optimized for transmission.
