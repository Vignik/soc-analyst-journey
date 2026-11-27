 # DAY 2 — OSI MODEL + TCP/IP MODEL
## SOC Analyst L1 Roadmap — Phase 1, Week 1

---

# 1. INTRODUCTION TO NETWORKING

**Definition:** A computer network is a group of connected devices that communicate and share information and resources.

Examples:
- Computers connected in an office.
- Mobile phones connected to Wi-Fi.
- Servers communicating over the internet.

**Why networking matters in SOC:**

SOC analysts investigate network activity to identify:
- Suspicious connections.
- Unauthorized access.
- Malware communication.
- Data exfiltration.
- Unusual traffic patterns.

# 2. OSI MODEL

## 2.1 What is the OSI Model?

**Full form:** Open Systems Interconnection.

**Kid-level explanation:** Imagine sending a parcel. It passes through different stages before reaching the receiver.

**Professional definition:** The OSI model is a conceptual framework that divides network communication into seven layers. Each layer performs specific functions to help devices communicate.

## 2.2 Seven Layers of the OSI Model

### Layer 7 — Application Layer

**Purpose:** Provides network services to applications used by people.

Examples:
- HTTP — Web communication.
- HTTPS — Secure web communication.
- DNS — Domain name resolution.
- SMTP — Sending email.
- FTP — File transfer.

**Example:** When you open a website, your browser uses application-layer protocols such as HTTP or HTTPS.

**SOC relevance:** Analysts investigate suspicious HTTP requests, DNS queries and application traffic.

### Layer 6 — Presentation Layer

**Purpose:** Handles data formatting, translation, encryption and compression.

Examples:
- Data encoding formats.
- Encryption and decryption functions.
- Compression.
- JPEG and other data formats.

**Example:** Data may need to be encoded or encrypted before being understood or processed by the receiving application.

**SOC relevance:** Understanding encryption helps analysts recognize why HTTPS traffic contents may not be visible in a packet capture.

Note: In real-world networking, encryption and presentation functions can be implemented across multiple layers. TLS does not always fit neatly into one OSI layer.

### Layer 5 — Session Layer

**Purpose:** Establishes, manages and terminates communication sessions between applications.

Functions:
- Session establishment.
- Session maintenance.
- Session termination.

**Example:** Managing a communication session between two applications.

**SOC relevance:** Understanding sessions helps when investigating communication patterns and session-related activity.

### Layer 4 — Transport Layer

**Purpose:** Provides end-to-end communication between applications running on different devices.

Main protocols:
- TCP
- UDP

Functions:
- Segmentation.
- Port addressing.
- Flow control.
- Error recovery and reliable delivery with TCP.

**Example:** A computer communicates with a web server using TCP port 443.

**SOC relevance:** Analysts investigate unusual ports, unexpected connections and suspicious TCP/UDP traffic.

### Layer 3 — Network Layer

**Purpose:** Handles logical addressing and routing packets between different networks.

Main protocol:
- IP (Internet Protocol).

Important concepts:
- Source IP address.
- Destination IP address.
- Routing.
- Packet forwarding.

Device:
- Router.

**Example:** A packet travels from your computer to a web server through multiple networks.

**SOC relevance:** Analysts investigate suspicious source and destination IP addresses, unusual network traffic and communication with malicious infrastructure.

### Layer 2 — Data Link Layer

**Purpose:** Handles communication between devices on the same local network.

Important concepts:
- MAC addresses.
- Frames.
- Switching.
- Error detection.

Examples:
- Ethernet.
- Wi-Fi MAC-layer communication.

Device:
- Switch (commonly operates at Layer 2).

**Example:** A switch forwards Ethernet frames within a local network using MAC address information.

**SOC relevance:** Analysts may investigate suspicious MAC addresses, ARP activity and unusual local network communication.

### Layer 1 — Physical Layer

**Purpose:** Transmits raw bits through a physical or wireless medium.

Examples:
- Ethernet cables.
- Fiber-optic cables.
- Radio signals.
- Network connectors.

**Example:** Electrical or optical signals carry data between connected devices.

**SOC relevance:** Helps understand the physical foundation of network communication and possible physical network disruptions.

## 2.3 OSI Model Summary

| Layer | Name | Main function |
|---|---|---|
| 7 | Application | Network services for applications |
| 6 | Presentation | Data formatting and encryption functions |
| 5 | Session | Manages communication sessions |
| 4 | Transport | End-to-end delivery |
| 3 | Network | IP addressing and routing |
| 2 | Data Link | Frames and MAC addressing |
| 1 | Physical | Transmits bits |

### Memory Trick

From Layer 7 to Layer 1:

**All People Seem To Need Data Processing.**

- A — Application
- P — Presentation
- S — Session
- T — Transport
- N — Network
- D — Data Link
- P — Physical

# 3. TCP/IP MODEL

## 3.1 What is the TCP/IP Model?

**Full form:** Transmission Control Protocol / Internet Protocol.

**Kid-level explanation:** TCP/IP is the set of communication rules that allows computers to exchange information over networks and the internet.

**Professional definition:** The TCP/IP model is a networking framework that describes how data is communicated across interconnected networks using protocols such as TCP and IP.

It is commonly represented using four layers.

## 3.2 Four Layers of TCP/IP Model

### Layer 4 — Application Layer

**Purpose:** Provides network services to applications.

Examples:
- HTTP
- HTTPS
- DNS
- SMTP
- FTP
- SSH
- DHCP

### Layer 3 — Transport Layer

**Purpose:** Provides communication between applications on different devices.

Protocols:
- TCP
- UDP

Functions:
- Segmentation.
- Port addressing.
- Reliable delivery with TCP.
- Connectionless communication with UDP.

### Layer 2 — Internet Layer

**Purpose:** Handles logical addressing and packet routing between networks.

Protocols:
- IPv4
- IPv6
- ICMP

Important concept:
- IP addressing and routing.

### Layer 1 — Network Access Layer

**Purpose:** Handles communication over the local network and physical transmission.

Examples:
- Ethernet.
- Wi-Fi.
- MAC addressing.
- Frames and physical media.

## 3.3 TCP/IP Model Summary

| Layer | Main function | Examples |
|---|---|---|
| Application | Application network services | HTTP, DNS, SMTP |
| Transport | End-to-end communication | TCP, UDP |
| Internet | IP addressing and routing | IPv4, IPv6, ICMP |
| Network Access | Local network transmission | Ethernet, Wi-Fi |

# 4. OSI MODEL vs TCP/IP MODEL

| OSI Model | TCP/IP Model |
|---|---|
| 7 layers | 4 commonly represented layers |
| Conceptual reference model | Practical networking protocol model |
| Separates Session and Presentation | Includes their functions in Application |
| Separates Physical and Data Link | Combines them in Network Access |
| Useful for understanding network functions | Used to describe real-world internet communication |

## 4.1 Layer Mapping

| OSI Layer | TCP/IP Layer |
|---|---|
| Application (7) | Application |
| Presentation (6) | Application |
| Session (5) | Application |
| Transport (4) | Transport |
| Network (3) | Internet |
| Data Link (2) | Network Access |
| Physical (1) | Network Access |

**Important:** The mapping is conceptual. Real protocols and implementations do not always fit perfectly into one OSI layer.

# 5. ENCAPSULATION

## 5.1 What is Encapsulation?

**Definition:** Encapsulation is the process of adding protocol information, such as headers, to data as it moves down the networking layers before transmission.

**Kid-level explanation:** Imagine putting a letter inside an envelope, then placing it inside a delivery package. Each stage adds information needed to deliver it.

## 5.2 Encapsulation Process

When data is sent from one computer to another:

1. Application Layer — Creates application data.
2. Transport Layer — Adds a TCP or UDP header.
3. Network Layer — Adds an IP header.
4. Data Link Layer — Adds a frame header and trailer.
5. Physical Layer — Transmits bits.

### Data Flow

Application Data  
↓  
TCP Segment / UDP Datagram  
↓  
IP Packet  
↓  
Data Link Frame  
↓  
Bits

## 5.3 Decapsulation

**Definition:** Decapsulation is the reverse process. The receiving device removes and processes the protocol information added at each layer to recover the original application data.

**Example:**

A server receives a network frame, processes the IP and transport headers, and delivers the application data to the correct application.

### Memory Trick

- Encapsulation = Adding information.
- Decapsulation = Removing and processing information.

# 6. DATA UNITS — DATA, SEGMENT, PACKET, FRAME AND BITS

Different networking layers use different names for the data they handle. These are called Protocol Data Units (PDUs).

| Layer | Data unit |
|---|---|
| Application | Data |
| Transport | Segment (TCP) / Datagram (UDP) |
| Network | Packet |
| Data Link | Frame |
| Physical | Bits |

## 6.1 Segment

A segment is the data unit commonly used by TCP at the Transport Layer.

It contains:
- TCP header.
- Application data.

## 6.2 Datagram

A UDP datagram is the data unit used by UDP at the Transport Layer.

It contains:
- UDP header.
- Application data.

## 6.3 Packet

A packet is the data unit at the Network Layer.

It contains:
- IP header.
- Transport-layer data.

It includes source and destination IP addresses.

## 6.4 Frame

A frame is the data unit at the Data Link Layer.

It contains:
- Frame header.
- Payload.
- Frame trailer (in Ethernet, commonly an FCS).

It includes MAC addressing information in Ethernet.

## 6.5 Bits

Bits are the binary values 0 and 1 transmitted through a physical or wireless medium.

### Easy Difference

- Segment = Transport Layer.
- Packet = Network Layer.
- Frame = Data Link Layer.
- Bits = Physical Layer.

# 7. COMMON NETWORK PROTOCOLS

A protocol is a set of rules that allows devices to communicate.

| Protocol | Purpose | Common port |
|---|---|---|
| HTTP | Web communication | TCP 80 |
| HTTPS | Secure web communication | TCP 443 |
| DNS | Domain name resolution | UDP/TCP 53 |
| DHCP | Automatic IP configuration | UDP 67, 68 |
| SSH | Secure remote access | TCP 22 |
| FTP | File transfer | TCP 20, 21 |
| SMTP | Sending email | TCP 25 |
| POP3 | Receiving email | TCP 110 |
| IMAP | Accessing email | TCP 143 |
| RDP | Remote desktop access | TCP/UDP 3389 |

**Important:** These are common default ports. Real deployments can use different ports or additional transport options.

## 7.1 HTTP

HTTP stands for Hypertext Transfer Protocol.

Purpose: Allows web browsers and web servers to communicate.

Default port: TCP 80.

Example: Opening a website using an HTTP URL.

## 7.2 HTTPS

HTTPS stands for Hypertext Transfer Protocol Secure.

Purpose: Protects HTTP communication using TLS encryption.

Default port: TCP 443.

Example: Logging into a website over an encrypted HTTPS connection.

## 7.3 DNS

DNS stands for Domain Name System.

Purpose: Converts domain names into IP addresses and supports other DNS records.

Example:

A user enters google.com. DNS helps resolve the domain name to an IP address.

Common port: 53 over UDP or TCP.

SOC relevance: Suspicious DNS queries may indicate malware communication or attempts to reach malicious domains.

## 7.4 DHCP

DHCP stands for Dynamic Host Configuration Protocol.

Purpose: Automatically provides network configuration to devices.

It can provide:
- IP address.
- Subnet mask.
- Default gateway.
- DNS server information.

Ports:
- UDP 67 — Server.
- UDP 68 — Client.

SOC relevance: DHCP logs can help identify which device was assigned an IP address at a particular time.

## 7.5 SSH

SSH stands for Secure Shell.

Purpose: Provides encrypted remote access to systems.

Default port: TCP 22.

Example: An administrator securely connects to a Linux server.

SOC relevance: Unexpected SSH login attempts may indicate brute-force activity.

## 7.6 FTP

FTP stands for File Transfer Protocol.

Purpose: Transfers files between systems.

Common ports:
- TCP 21 — Control connection.
- TCP 20 — Traditional active-mode data connection.

Important: Standard FTP does not encrypt credentials or file contents by default.

SOC relevance: Investigate unexpected FTP use and possible unauthorized file transfers.

## 7.7 SMTP

SMTP stands for Simple Mail Transfer Protocol.

Purpose: Sends email between mail clients and servers or between mail servers.

Common ports:
- TCP 25 — Mail transfer.
- TCP 587 — Message submission.
- TCP 465 — Common implicit TLS submission.

SOC relevance: Investigate suspicious outbound email, spam and phishing-related activity.

## 7.8 RDP

RDP stands for Remote Desktop Protocol.

Purpose: Allows remote access to a Windows desktop.

Common port: TCP/UDP 3389.

SOC relevance: Unexpected RDP connections and repeated login failures may indicate brute-force attempts or unauthorized remote access.

# 8. REAL SOC ANALYST EXAMPLE

## Scenario: Suspicious Network Connection

A SIEM generates an alert:

- Source IP: 192.168.1.10
- Destination IP: 185.XX.XX.XX
- Destination port: 443
- Protocol: TCP
- Activity: Unusual outbound connection
- User: employee01

### How an L1 SOC analyst investigates

1. Identify the source and destination IP addresses.
2. Identify the destination port and protocol.
3. Check whether the destination is known or suspicious.
4. Review firewall and proxy logs.
5. Check DNS queries associated with the destination.
6. Look for repeated connections or unusual traffic patterns.
7. Correlate the activity with endpoint alerts.
8. Document findings and escalate if suspicious.

### Which OSI layers help?

- Layer 7: Application traffic and web requests.
- Layer 4: TCP and destination port.
- Layer 3: Source and destination IP addresses.
- Layer 2: MAC address and local network communication.

**Important:** An unusual connection alone does not prove malicious activity. Validate evidence before deciding.

# 9. INTERVIEW QUESTIONS AND ANSWERS

**Q1. What is the OSI model?**

The OSI model is a conceptual networking framework that divides communication into seven layers.

**Q2. Name the seven OSI layers.**

Application, Presentation, Session, Transport, Network, Data Link and Physical.

**Q3. What is the TCP/IP model?**

It is a networking framework commonly represented with four layers that describes how devices communicate using TCP/IP protocols.

**Q4. How many layers are in the TCP/IP model?**

Four commonly represented layers.

**Q5. What is the difference between OSI and TCP/IP?**

OSI has seven layers and is mainly a reference model. TCP/IP has four commonly represented layers and describes the protocol architecture used for internet communication.

**Q6. What is encapsulation?**

Encapsulation is the process of adding protocol information to data as it moves down the networking layers before transmission.

**Q7. What is decapsulation?**

Decapsulation is the reverse process of processing and removing protocol information at the receiving device.

**Q8. What is a TCP segment?**

It is the Transport Layer data unit used by TCP.

**Q9. What is a packet?**

A packet is the Network Layer data unit containing an IP header and payload.

**Q10. What is a frame?**

A frame is the Data Link Layer data unit used to transfer information across a local network link.

**Q11. What is DNS?**

DNS translates domain names into IP addresses and provides other domain-related records.

**Q12. What is DHCP?**

DHCP automatically assigns IP configuration to network devices.

**Q13. What is the difference between HTTP and HTTPS?**

HTTP provides web communication. HTTPS protects HTTP communication using TLS encryption.

**Q14. What is SSH?**

SSH provides encrypted remote access to systems.

**Q15. Which OSI layer is responsible for routing?**

Layer 3 — Network Layer.

**Q16. Which OSI layer uses MAC addresses?**

Layer 2 — Data Link Layer.

**Q17. Which OSI layer uses TCP and UDP?**

Layer 4 — Transport Layer.

---

# 10. QUICK REVISION

OSI = 7 layers.

TCP/IP = 4 commonly represented layers.

Application = Network services for applications.

Presentation = Formatting and encryption functions.

Session = Manages sessions.

Transport = TCP and UDP.

Network = IP addressing and routing.

Data Link = Frames and MAC addresses.

Physical = Bits and signals.

Encapsulation = Adding headers and other protocol information.

Decapsulation = Processing and removing protocol information.

TCP = Reliable, connection-oriented transport.

UDP = Connectionless transport.

DNS = Domain name resolution.

DHCP = Automatic IP configuration.

HTTP = Web communication.

HTTPS = Secure web communication.

SSH = Secure remote access.

FTP = File transfer.

SMTP = Sending email.

RDP = Remote desktop.

Segment = TCP Transport Layer data unit.

Datagram = UDP Transport Layer data unit.

Packet = Network Layer data unit.

Frame = Data Link Layer data unit.

Bits = Physical Layer data unit.



**End of Day 2 — OSI Model + TCP/IP Model**