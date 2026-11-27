# DAY 3 — IP ADDRESSING AND SUBNETTING
## SOC Analyst L1 | Phase 1 — Week 1

---

## 1. What is an IP Address?

**Definition:** An IP (Internet Protocol) address is a logical address assigned to a device on a network to identify it and enable communication.

**Example:** `192.168.1.10`

**Purpose:**
- Identifies devices on a network.
- Helps devices communicate.
- Helps route data between networks.

---

## 2. IPv4 Addressing

**Definition:** IPv4 is a 32-bit addressing system used to identify devices on IP networks.

An IPv4 address contains four octets separated by dots.

Example:

`192.168.1.10`

Each octet contains 8 bits.

Total: 4 × 8 = 32 bits.

Each octet has a value from 0 to 255.

**Binary representation:**

`192.168.1.10`

`11000000.10101000.00000001.00001010`

---

## 3. Public IP vs Private IP

### Public IP

A public IP address is globally routable and is used to communicate across the internet.

Example: A company's internet-facing web server may have a public IP address.

### Private IP

A private IP address is used inside private networks and is not directly routable across the public internet.

Private IPv4 ranges:

| Class | Private IP range |
|---|---|
| Class A | 10.0.0.0 – 10.255.255.255 |
| Class B | 172.16.0.0 – 172.31.255.255 |
| Class C | 192.168.0.0 – 192.168.255.255 |

**Important:** These are historical class labels for the private ranges. Modern networks use CIDR.

**SOC relevance:**
- Private IPs commonly identify internal devices.
- Public IPs can identify internet-facing systems or external communication endpoints.
- Analysts examine both source and destination IPs during investigations.

---

## 4. Network ID and Host ID

An IP address can be divided into two logical parts:

### Network ID
Identifies the network to which a device belongs.

### Host ID
Identifies a device within that network.

Example:

IP address: `192.168.1.10`

Subnet mask: `255.255.255.0`

- Network portion: `192.168.1`
- Host portion: `10`
- Network address: `192.168.1.0`

The subnet mask determines which bits belong to the network and which belong to the host.

---

## 5. Subnet Mask

**Definition:** A subnet mask identifies the network portion and host portion of an IPv4 address.

Example:

IP address: `192.168.1.10`

Subnet mask: `255.255.255.0`

This means the first 24 bits represent the network portion.

CIDR notation: `/24`

**Common subnet masks:**

| CIDR | Subnet mask |
|---|---|
| /8 | 255.0.0.0 |
| /16 | 255.255.0.0 |
| /24 | 255.255.255.0 |
| /25 | 255.255.255.128 |
| /26 | 255.255.255.192 |
| /27 | 255.255.255.224 |
| /28 | 255.255.255.240 |
| /30 | 255.255.255.252 |

---

## 6. CIDR Notation

**Full form:** Classless Inter-Domain Routing.

**Definition:** CIDR represents the network portion of an IP address using a slash followed by the number of network bits.

Example:

`192.168.1.10/24`

Here:
- IPv4 address = 192.168.1.10
- `/24` = 24 network bits
- Remaining 8 bits = host bits

CIDR allows flexible allocation of IP addresses without relying on traditional address classes.

---

## 7. Subnetting

**Definition:** Subnetting is the process of dividing a larger IP network into smaller logical networks called subnets.

**Why subnetting is used:**
- Better IP address management.
- Reduces broadcast domains when separate subnets are used.
- Improves network organization.
- Helps isolate network segments.
- Supports network security design.

### Important formulas

For a conventional IPv4 subnet:

Host bits = 32 − Prefix length

Total addresses = 2^(Host bits)

Usable host addresses = Total addresses − 2

The usable-host formula applies to ordinary subnets where the network and broadcast addresses are reserved. Special cases such as `/31` and `/32` have different usage rules.

### Example 1: /24 subnet

Network: `192.168.1.0/24`

- Network bits = 24
- Host bits = 8
- Total addresses = 2^8 = 256
- Usable host addresses = 256 − 2 = 254
- Network address = 192.168.1.0
- Broadcast address = 192.168.1.255
- Usable range = 192.168.1.1 – 192.168.1.254

### Example 2: /25 subnet

Network: `192.168.1.0/25`

- Network bits = 25
- Host bits = 7
- Total addresses = 2^7 = 128
- Usable host addresses = 126
- Network address = 192.168.1.0
- Broadcast address = 192.168.1.127
- Usable range = 192.168.1.1 – 192.168.1.126

### Example 3: /26 subnet

Network: `192.168.1.0/26`

- Network bits = 26
- Host bits = 6
- Total addresses = 64
- Usable host addresses = 62
- Network address = 192.168.1.0
- Broadcast address = 192.168.1.63
- Usable range = 192.168.1.1 – 192.168.1.62

---

## 8. Default Gateway

**Definition:** A default gateway is the device, usually a router or Layer 3 switch, that forwards traffic from a local network to other networks when no more specific route is available.

Example:

- Computer IP: `192.168.1.10`
- Subnet mask: `255.255.255.0`
- Default gateway: `192.168.1.1`

When the computer wants to communicate with an IP outside its local subnet, it sends the traffic to the default gateway.

**SOC relevance:** Incorrect gateway settings can cause connectivity issues. Analysts may investigate unusual gateway configurations as part of network troubleshooting.

---

## 9. Useful Windows Commands

### View IP configuration

```bash
ipconfig
```

Displays IP address, subnet mask and default gateway.

### View detailed IP configuration

```bash
ipconfig /all
```

Displays detailed network configuration, including DNS and physical address information.

### Test connectivity

```bash
ping 8.8.8.8
```

Tests connectivity to the destination IP using ICMP Echo requests.

### View network routes

```bash
route print
```

Displays the system's routing table.

### Trace network path

```bash
tracert example.com
```

Displays the route taken towards the destination.

---

## 10. SOC Analyst Real-World Example

### Scenario: Suspicious Internal Communication

A SIEM generates an alert:

- Source IP: `192.168.1.25`
- Destination IP: `192.168.1.50`
- Activity: Unusual internal connection
- Protocol: TCP

### L1 Analyst Investigation

1. Identify the source and destination IP addresses.
2. Determine whether the IPs belong to private or public ranges.
3. Identify the subnet of each device.
4. Check firewall and endpoint logs.
5. Review the destination port and connection history.
6. Determine whether the communication is expected.
7. Document findings and escalate suspicious activity.

**Important:** Internal communication is not automatically safe. Attackers can move between devices inside an organization's network.

---

## 11. Interview Questions and Answers

**Q1. What is an IP address?**

An IP address is a logical address used to identify devices and enable communication across IP networks.

**Q2. What is IPv4?**

IPv4 is a 32-bit addressing system represented using four decimal octets.

**Q3. What is the difference between public and private IP addresses?**

Public IPs are globally routable, while private IPs are used inside private networks and are not directly routable over the public internet.

**Q4. What is a subnet mask?**

A subnet mask identifies the network and host portions of an IPv4 address.

**Q5. What is CIDR?**

CIDR is a method of representing IP network prefixes using slash notation, such as `/24`.

**Q6. What is subnetting?**

Subnetting divides a larger network into smaller logical networks.

**Q7. What is a default gateway?**

A default gateway forwards traffic from a local network to other networks when no more specific route exists.

**Q8. How many usable hosts are available in a normal /24 subnet?**

254 usable host addresses.

**Q9. What is a network address?**

It identifies a particular IP network or subnet.

**Q10. What is a broadcast address?**

It is the IPv4 address used to send traffic to all hosts on a particular subnet.

---

## 12. Quick Revision

- IPv4 = 32 bits.
- One octet = 8 bits.
- One octet ranges from 0 to 255.
- Public IP = Globally routable.
- Private IP = Used in private networks.
- Subnet mask = Separates network and host portions.
- CIDR = Prefix notation such as `/24`.
- Subnetting = Dividing networks.
- Network ID = Identifies the network.
- Host ID = Identifies a device within the network.
- Default gateway = Path to other networks.
- `/24` = 256 total addresses, normally 254 usable host addresses.

---

 

**End of Day 3 — IP Addressing and Subnetting**