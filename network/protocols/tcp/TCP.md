# Transmission Control Protocol (TCP)

## Introduction

Transmission Control Protocol (TCP) is a core protocol of the Internet Protocol Suite. It is a transport layer protocol built on top of the Internet Protocol (IP) and is used in conjunction with IP to provide a reliable data transmission service.

This means that TCP uses IP for the actual delivery of data packets. TCP relies on IP to move packets across the network from one device to another.

## What is TCP?

TCP is designed to ensure that data is reliably transmitted between devices over a network. It breaks data into smaller packets, numbers them in sequence, and ensures they are received in the correct order at the destination. If any packets are lost or arrive out of order, TCP can retransmit them, ensuring data integrity and reliability.

![](https://cdn-images-1.medium.com/max/900/1*95_hwrT21l9xpZwEI4nfbw.png)

## Why is TCP Important?

When sending files like images or emails, a single IP packet may not suffice. Hence, data needs to be divided into multiple packets, increasing the risk of packets not reaching their destination or arriving in the wrong order. TCP addresses these issues by providing mechanisms for:
- Sequencing packets
- Retransmitting lost packets
- Reordering out-of-sequence packets
- Ensuring data integrity with error-checking

## How TCP Works

### 1. Connection Establishment (Three-Way Handshake)

To start communication, a connection is established between the sender and receiver using a three-way handshake:
1. The sender sends a SYN (synchronize) packet to the receiver.
2. The receiver responds with a SYN-ACK (synchronize-acknowledgment) packet.
3. The sender sends an ACK (acknowledgment) packet to complete the connection.

### 2. Data Transmission

Once the connection is established, data transmission occurs as follows:
1. The sender divides data into TCP segments, each containing a sequence number, source port number, destination port number, checksums for error detection, etc.
2. TCP segments are sent over the network to the destination IP address and port number. TCP uses flow control to prevent the sender from overwhelming the receiver with too much data at once.
3. The receiver reassembles the TCP segments into the original data. If a segment is lost or corrupted, the receiver requests retransmission from the sender.

### 3. Connection Termination (Four-Way Handshake)

After data transmission is complete, the connection is terminated using a four-way handshake:
1. The sender sends a FIN (finish) packet to the receiver.
2. The receiver acknowledges the FIN with an ACK packet and then sends its own FIN packet.
3. The sender responds with an ACK packet to acknowledge the receiver's FIN packet.

![](https://www.cloudflare.com/img/learning/cdn/tls-ssl/tcp-handshake-diagram.png)

## Features of TCP

- **Connection-Oriented**: A connection must be established between devices before data transfer.
- **Reliable**: Ensures data is transmitted accurately with error-checking and retransmission.
- **Ordered**: Maintains the correct order of data packets.
- **Flow Control**: Prevents sender from overwhelming the receiver.

## Use Cases of TCP

- **Email Applications**: Email clients like Outlook or Gmail use the Simple Mail Transfer Protocol (SMTP) over TCP to send and receive emails.
- **File Transfer**: Protocols like FTP (File Transfer Protocol) or SFTP (Secure File Transfer Protocol) use TCP for transferring files.
- **Remote Desktop**: Remote desktop software uses TCP to transmit data and user inputs between the client and server.

## What Next?

### Related Topics

- User Datagram Protocol (UDP)
- Internet Protocol (IP)
- Simple Mail Transfer Protocol (SMTP)
- File Transfer Protocol (FTP)

### Topics for Deeper Understanding

- TCP Congestion Control
- TCP Flow Control Mechanisms
- Differences between TCP and UDP
- Detailed Study of TCP Handshake Processes
- Error Detection and Correction in TCP
