# Day 5 — Network Services: DNS, DHCP, Firewall, NAT & VPN

## 1. DNS (Domain Name System)

### What is DNS?

**Beginner definition:** DNS converts website names into IP addresses.

**Professional definition:** DNS is a distributed naming system that translates human-readable domain names into IP addresses, allowing devices to locate network services.

### Why is DNS needed?

Computers communicate using IP addresses, but humans remember domain names more easily.

Example:

- Domain: `google.com`
- IP address: `142.250.x.x` (example format)

DNS helps find the IP address associated with a domain.

### How DNS works

1. User enters `google.com` in a browser.
2. The device checks its local DNS cache.
3. If not cached, it contacts a DNS resolver.
4. The resolver finds the required DNS record.
5. The IP address is returned.
6. The browser connects to the destination server.

![alt text](image-2.png)

### Common DNS records

| Record | Purpose                                                                 |
| ------ | ----------------------------------------------------------------------- |
| A      | Maps domain to IPv4 address                                             |
| AAAA   | Maps domain to IPv6 address                                             |
| CNAME  | Alias of another domain                                                 |
| MX     | Identifies mail servers                                                 |
| NS     | Identifies authoritative name servers                                   |
| TXT    | Stores text information, often used for verification and email security |

### DNS security threats

- **DNS Spoofing:** Providing false DNS responses.
- **DNS Tunneling:** Hiding data or communication inside DNS queries and responses.
- **DNS Poisoning:** Corrupting DNS cache information.
- **Malicious Domains:** Domains used for phishing, malware or command-and-control communication.

### SOC Analyst example

An endpoint repeatedly sends DNS queries to a suspicious domain.

A SOC analyst should:

1. Identify the source device.
2. Check the queried domain.
3. Review DNS logs and query frequency.
4. Check threat-intelligence sources.
5. Look for connections to the resolved IP.
6. Escalate or contain according to the incident response procedure.

### Kali Linux commands

```bash
nslookup example.com
```

Finds the IP address associated with a domain.

```bash
dig example.com
```

Displays detailed DNS query information.

```bash
cat /etc/resolv.conf
```

Displays configured DNS resolver information.

---

## 2. DHCP (Dynamic Host Configuration Protocol)

### What is DHCP?

**Beginner definition:** DHCP automatically provides IP configuration to devices when they connect to a network.

**Professional definition:** DHCP is a client-server protocol that dynamically assigns IP addresses and other network configuration parameters to clients.

### Why is DHCP needed?

Without DHCP, an administrator may need to configure every device manually.

DHCP can automatically provide:

- IP address
- Subnet mask
- Default gateway
- DNS server

### DHCP DORA process

DORA represents the four steps of DHCP:

1. **Discover:** Client searches for a DHCP server.
2. **Offer:** Server offers an IP address.
3. **Request:** Client requests the offered address.
4. **Acknowledge:** Server confirms the assignment.

![alt text](image-3.png)   ![alt text](image-4.png)

### DHCP security threats

**Rogue DHCP Server:**
An unauthorized DHCP server provides incorrect network configuration.

Possible consequences:

- Incorrect gateway assignment.
- Malicious DNS server assignment.
- Traffic redirection.
- Man-in-the-middle opportunities.

### SOC Analyst example

A workstation suddenly receives an unfamiliar default gateway and DNS server.

The analyst should:

1. Check the workstation's IP configuration.
2. Identify the DHCP server.
3. Compare it with authorized DHCP servers.
4. Review network logs.
5. Escalate suspicious activity.

### Kali Linux commands

```bash
ip addr
```

Displays network interfaces and IP addresses.

```bash
ip route
```

Displays routing information, including the default gateway.

---

## 3. Firewall

### What is a Firewall?

**Beginner definition:** A firewall acts like a security guard that allows or blocks network traffic.

**Professional definition:** A firewall is a network security control that monitors and filters incoming and outgoing traffic based on configured security rules.

### Why is a firewall needed?

A firewall helps:

- Block unauthorized connections.
- Restrict suspicious traffic.
- Allow approved services.
- Enforce network security policies.
- Monitor network communication.

### How a firewall works

A firewall evaluates traffic against configured rules.

Example:

| Traffic                   | Action               |
| ------------------------- | -------------------- |
| Approved HTTPS traffic    | Allow                |
| Unauthorized connection   | Block                |
| Suspicious source IP      | Block or investigate |
| Approved internal service | Allow                |


 

### Types of firewalls 

1. **Packet-filtering firewall:** Filters traffic using IP addresses, ports and protocols.
2. **Stateful firewall:** Tracks connection states and makes decisions based on connection context.
3. **Application-layer firewall:** Inspects application-level traffic.
4. **Next-Generation Firewall (NGFW):** Combines traditional firewall features with advanced inspection and security capabilities.

![alt text](image-5.png)
![alt text](image-6.png)
![alt text](image-7.png)
### Firewall security example

Suppose an external IP repeatedly attempts to connect to an internal server over an unauthorized port.

The firewall may block the connection and generate a log.

A SOC analyst should:

1. Identify the source and destination IP.
2. Identify the destination port and protocol.
3. Review firewall logs.
4. Check whether the activity is expected.
5. Investigate repeated attempts.
6. Follow the organization's response procedure.

### Kali Linux command

```bash
sudo ufw status
```

Checks UFW firewall status, if UFW is installed and configured.

**Important:** Kali may use other firewall management tools. UFW is not guaranteed to be active.

---

## 4. NAT (Network Address Translation)

### What is NAT?

**Beginner definition:** NAT allows devices using private IP addresses to communicate with external networks by translating addresses.

**Professional definition:** NAT modifies IP address information in packet headers as traffic passes through a router or network gateway.

### Why is NAT needed?

Private IP addresses are not directly routable across the public internet.

NAT helps internal devices communicate with external networks using public IP addressing.

### Example

Imagine a home network:

| Device  | Private IP   |
| ------- | ------------ |
| Laptop  | 192.168.1.10 |
| Mobile  | 192.168.1.11 |
| Desktop | 192.168.1.12 |

These devices can share one public IP address when accessing the internet through a NAT-enabled router.

### NAT diagram

![alt text](image-8.png)

### Types of NAT

1. **Static NAT:** One private IP maps to one public IP.
2. **Dynamic NAT:** Private IP addresses are mapped to available public IP addresses from a pool.
3. **PAT (Port Address Translation):** Multiple internal devices share a public IP using different port numbers.

![alt text](image-9.png)

### Important: NAT vs Firewall

| NAT                                              | Firewall                           |
| ------------------------------------------------ | ---------------------------------- |
| Translates IP addresses                          | Filters network traffic            |
| Helps conserve public IP addresses               | Enforces traffic security rules    |
| Does not automatically provide complete security | Can block unauthorized connections |

**Remember:** NAT is not a replacement for a firewall.

### SOC Analyst example

A SOC analyst sees multiple internal devices communicating with an external IP through one public IP.

The analyst may need NAT translation logs to identify which internal device initiated the connection.

---

## 5. VPN (Virtual Private Network)

### What is a VPN?

**Beginner definition:** A VPN creates a protected connection over a network such as the internet.

**Professional definition:** A VPN establishes an encrypted communication tunnel between endpoints or networks over an underlying network.

### Why is VPN used?

- Secure remote access.
- Protect communication over untrusted networks.
- Connect different office networks.
- Support remote employees.

### Types of VPN

**1. Remote Access VPN**

Connects an individual user or device to an organization's network.

Example: An employee working from home securely connects to the company network.

**2. Site-to-Site VPN**

Connects two or more networks securely.

Example: Connecting a company's Hyderabad office to its Bengaluru office.

### VPN diagram

![alt text](image-10.png)

### VPN security risks

- Stolen VPN credentials.
- Unauthorized remote access.
- Suspicious login locations.
- Unusual login times.
- Compromised remote devices.
- Repeated failed VPN authentication attempts.

### SOC Analyst example

A VPN account successfully logs in from an unusual location at an unusual time.

The analyst should:

1. Identify the account.
2. Check login time and source IP.
3. Review authentication logs.
4. Compare with the user's normal login pattern.
5. Check for MFA failures or unusual activity.
6. Escalate and follow the incident response procedure.

 

## 6. How DNS, DHCP, Firewall, NAT and VPN Work Together

These services perform different jobs but work together in a network.

### Example: Employee accessing a website

1. **DHCP:** The employee's device receives an IP address, gateway and DNS configuration.
2. **DNS:** The device resolves the website domain into an IP address.
3. **Firewall:** Network traffic is checked against security rules.
4. **NAT:** The internal private IP may be translated for internet communication.
5. **VPN:** If the employee is remotely accessing company resources, a VPN may provide an encrypted tunnel.

 
 
---

## 7. SOC Analyst Quick Reference

| Service  | Main Function                 | SOC Security Concern                |
| -------- | ----------------------------- | ----------------------------------- |
| DNS      | Domain-to-IP resolution       | DNS tunneling, malicious domains    |
| DHCP     | Automatic IP configuration    | Rogue DHCP servers                  |
| Firewall | Traffic filtering             | Unauthorized connections            |
| NAT      | Address translation           | Identifying internal source devices |
| VPN      | Protected remote connectivity | Stolen credentials, unusual logins  |

## 8. Important SOC Investigation Scenarios

### Scenario 1: Suspicious DNS activity

**Observation:** A computer sends repeated DNS requests to a strange domain.

**Possible concern:** Malware communication or DNS tunneling.

**Action:** Investigate the domain, source endpoint, DNS logs and related connections.

### Scenario 2: Rogue DHCP server

**Observation:** A device receives an unexpected gateway and DNS server.

**Possible concern:** Unauthorized DHCP server.

**Action:** Identify the DHCP server and validate its authorization.

### Scenario 3: Firewall alerts

**Observation:** Repeated blocked connections to an internal server.

**Possible concern:** Port scanning or unauthorized access attempts.

**Action:** Review source IP, destination port, frequency and related activity.

### Scenario 4: NAT investigation

**Observation:** A suspicious public IP is associated with multiple internal users.

**Possible concern:** Suspicious outbound communication from an internal endpoint.

**Action:** Use NAT translation logs and timestamps to identify the originating internal device.

### Scenario 5: VPN login anomaly

**Observation:** A user account logs in from an unusual location.

**Possible concern:** Compromised credentials.

**Action:** Verify the user, source IP, login history, MFA events and related activity.

---

## 9. Kali Linux Practical Commands

Run these commands in your Kali Linux terminal.

```bash
ip addr
```

View network interfaces and IP addresses.

```bash
ip route
```

View routing table and default gateway.

```bash
cat /etc/resolv.conf
```

View DNS resolver configuration.

```bash
nslookup example.com
```

Perform a DNS lookup.

```bash
dig example.com
```

Inspect DNS query information.

```bash
ping -c 4 example.com
```

Send four ICMP echo requests to test connectivity.

```bash
sudo ufw status
```

Check UFW firewall status, if available.

---

## 10. Important Interview Questions

**Q1. What is DNS?**

DNS translates domain names into IP addresses.

**Q2. What is DHCP?**

DHCP automatically assigns IP configuration to network devices.

**Q3. Explain DORA.**

Discover, Offer, Request and Acknowledge.

**Q4. What is a rogue DHCP server?**

An unauthorized DHCP server that provides incorrect or potentially malicious network configuration.

**Q5. What is a firewall?**

A security control that monitors and filters network traffic based on configured rules.

**Q6. What is NAT?**

NAT translates IP address information as traffic passes through a network gateway.

**Q7. Is NAT a firewall?**

No. NAT translates addresses; a firewall filters traffic.

**Q8. What is a VPN?**

A VPN creates a protected communication tunnel over an underlying network.

**Q9. What would you investigate if a user has an unusual VPN login?**

Check the account, source IP, location, timestamp, authentication logs, MFA activity and normal login patterns.

**Q10. What is DNS tunneling?**

DNS tunneling uses DNS queries and responses to carry data or communication that may evade normal network monitoring.

---

## 11. Final Revision

- DNS = Resolves domain names.
- DHCP = Assigns IP configuration.
- DORA = Discover, Offer, Request, Acknowledge.
- Firewall = Filters network traffic.
- NAT = Translates IP addresses.
- PAT = Allows multiple devices to share a public IP using ports.
- VPN = Creates a protected communication tunnel.
- Rogue DHCP = Unauthorized DHCP server.
- DNS tunneling = Hiding data or communication in DNS traffic.

 

 