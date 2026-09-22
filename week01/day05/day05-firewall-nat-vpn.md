# Day 5 — Firewall + NAT + VPN

## 1. Firewall

### What is a Firewall?

A firewall is a network security control that monitors and controls network traffic based on predefined rules.

It can decide whether traffic should be:

- ALLOWED
- DENIED
- DROPPED

A firewall can examine information such as:

- Source IP address
- Destination IP address
- Source port
- Destination port
- Protocol
- Connection state

Example:

    Source: 10.0.0.15
    Destination: 142.250.x.x
    Destination Port: 443
    Protocol: TCP
    Action: ALLOW

The firewall checks its rules and decides whether the connection should be permitted.

Simple idea:

    Traffic
       ↓
    Firewall
       ↓
    Check rules
       ↓
    ALLOW / DENY


### Inbound Traffic

Inbound traffic is traffic coming INTO a network or system.

Example:

    Internet
        |
        | Connection
        ↓
    Company Server

From the company's perspective, this is inbound traffic.

Example:

    Source: 185.10.20.30
    Destination: 10.0.0.20
    Destination Port: 443

The firewall checks whether the incoming connection is allowed.

Example:

    Internet → Company Server : 443 → ALLOW
    Internet → Internal Server : 3389 → DENY

Inbound means:

    OUTSIDE → INSIDE


### Outbound Traffic

Outbound traffic is traffic going OUT of a network or system.

Example:

    Employee Laptop
          |
          | HTTPS
          ↓
       Internet

This is outbound traffic.

Example:

    Source: 10.0.0.15
    Destination: 142.250.x.x
    Destination Port: 443

The firewall can also control outbound traffic.

Outbound traffic is important for SOC analysts because a compromised computer may try to communicate with an attacker's server.

Example:

    Infected Laptop
          |
          | Outbound connection
          ↓
    Attacker's Server

The SOC analyst may investigate the destination, frequency, timing and other characteristics of the connection.

Outbound means:

    INSIDE → OUTSIDE


### Firewall Rules

Firewalls use rules to determine whether traffic should be allowed or denied.

A simplified firewall rule can contain:

    Source
    Destination
    Port
    Protocol
    Action

Example:

    Source              Destination       Port    Action
    ----------------------------------------------------
    Internal Network    Internet          443     ALLOW
    Internet            Internal Network  22      DENY
    Internet            Web Server        443     ALLOW
    Internal Network    DNS Server         53     ALLOW

The firewall essentially asks:

    WHO is connecting?
        ↓
    Source IP

    WHERE are they connecting?
        ↓
    Destination IP

    HOW are they connecting?
        ↓
    Protocol + Port

    WHAT should happen?
        ↓
    ALLOW / DENY


### Important Ports

Some important ports for SOC fundamentals are:

| Port | Service | Common Use |
|------|---------|------------|
| 22 | SSH | Secure remote administration |
| 25 | SMTP | Email transfer |
| 53 | DNS | Domain name resolution |
| 80 | HTTP | Web traffic |
| 443 | HTTPS | Encrypted web traffic |
| 3389 | RDP | Windows Remote Desktop |
| 445 | SMB | Windows file/network sharing |

Example:

    192.168.1.10:52344 → 8.8.8.8:443

Here:

    Source IP = 192.168.1.10
    Source Port = 52344
    Destination IP = 8.8.8.8
    Destination Port = 443

Port 443 is commonly used for HTTPS.

The source port 52344 is an example of a client-side ephemeral port.


### Stateful Firewall

A stateful firewall tracks the state of active network connections.

Example:

    Laptop
       |
       | TCP connection
       ↓
    Firewall
       |
       ↓
    Website

The firewall keeps information about the connection.

If the website sends a response:

    Website
       |
       | Response
       ↓
    Firewall
       |
       ↓
    Laptop

The firewall can recognize that the response belongs to an existing connection that was initiated by the laptop.

Simple definition:

> A stateful firewall tracks the state of network connections.


### Stateless Firewall

A stateless firewall evaluates network packets individually against predefined rules.

Conceptually:

    Packet arrives
          ↓
    Check packet information
          ↓
    Check firewall rules
          ↓
    ALLOW / DENY

A stateless firewall does not maintain connection state in the same way as a stateful firewall.

Simple definition:

> A stateless firewall evaluates packets individually using configured rules.


### Stateful vs Stateless

| Stateful Firewall | Stateless Firewall |
|-------------------|--------------------|
| Tracks connection state | Evaluates packets individually |
| Understands active connections | Does not maintain connection state in the same way |
| Can recognize traffic belonging to an existing connection | Mainly checks packet information against rules |
| Useful for connection-aware filtering | Simple and rule-based packet filtering |

Easy memory:

    STATEFUL
    = Tracks connections

    STATELESS
    = Evaluates packets individually


---

## 2. NAT

### What is NAT?

NAT stands for:

    Network Address Translation

NAT translates network addressing information between different address spaces.

In a common private IPv4 network, NAT allows devices using private IP addresses to communicate through a public IP address.

Basic idea:

    Private IP
        ↓
       NAT
        ↓
    Public IP
        ↓
     Internet

Example:

    Laptop
    192.168.1.10
          |
          ↓
        NAT
          |
          ↓
    203.0.113.50
          |
          ↓
       Internet

The important point is:

> NAT performs address translation.


### Private IP

A private IP address is used inside private networks such as home, college or company networks.

Common private IPv4 ranges are:

    10.0.0.0/8
    172.16.0.0/12
    192.168.0.0/16

Examples:

    10.0.0.10
    172.16.5.20
    192.168.1.50

Example company network:

    Laptop   → 10.0.0.10
    Server   → 10.0.0.20
    Printer  → 10.0.0.30

These addresses are used within the internal network.


### Public IP

A public IP address is a globally routable IP address used for communication across the public Internet.

Example:

    203.0.113.50

In a typical network using NAT:

    Internal devices
          ↓
    Private IP addresses
          ↓
        NAT
          ↓
    Public IP address
          ↓
       Internet

The public IP is the address used for Internet connectivity from outside the private network.


### Why NAT is Used

One major reason NAT is useful is IPv4 address conservation.

A company may have many internal devices:

    Laptop 1 → 10.0.0.10
    Laptop 2 → 10.0.0.11
    Laptop 3 → 10.0.0.12
    Laptop 4 → 10.0.0.13

Instead of requiring a separate public IPv4 address for every internal device, NAT can allow many devices to share public IPv4 connectivity.

Example:

    Laptop 1 ─┐
    Laptop 2 ─┤
    Laptop 3 ─┤
    Laptop 4 ─┤
              ↓
             NAT
              ↓
       Public IP
       203.0.113.50
              ↓
           Internet

NAT therefore helps conserve public IPv4 addresses and allows private networks to communicate with the Internet.


### NAT + Ports

NAT can also translate port information.

Example:

    Internal device:

    192.168.1.10:50000

    connects to:

    Website:

    93.184.216.34:443

The NAT device may translate the internal source to:

    203.0.113.50:40001

Conceptually:

    192.168.1.10:50000
             |
             ↓
            NAT
             |
             ↓
    203.0.113.50:40001
             |
             ↓
    93.184.216.34:443

This allows multiple internal connections to share a public IPv4 address.

A common form of this is called PAT (Port Address Translation) or NAT overload.


### NAT vs Firewall

NAT and a firewall are different technologies.

NAT:

    Translates addresses
    and commonly ports

Firewall:

    Controls network traffic
    using security rules

Example:

    Internal Network
           |
           ↓
        Firewall
           |
           ↓
          NAT
           |
           ↓
        Internet

A device can perform both firewalling and NAT, but NAT itself is not a replacement for a firewall.

Easy memory:

    Firewall = Traffic control
    NAT      = Address translation


---

## 3. VPN

### What is a VPN?

VPN stands for:

    Virtual Private Network

A VPN creates a logical connection or tunnel between a device and a VPN endpoint.

Encryption is commonly used to protect traffic travelling through the VPN tunnel.

Basic model:

    Your Device
         |
         | Encrypted Tunnel
         ↓
     VPN Server
         |
         ↓
      Internet

The VPN server becomes an intermediary between the device and other network destinations.


### Encrypted Tunnel

An encrypted tunnel protects traffic between the VPN client and VPN endpoint.

Without a VPN:

    Device
       |
       ↓
    Network
       |
       ↓
    Internet

With a VPN:

    Device
       |
       | Encrypted traffic
       ↓
    VPN Server
       |
       ↓
    Internet

The traffic travelling through the VPN tunnel is protected using encryption.

For example:

    Laptop
       |
       | VPN encrypted tunnel
       ↓
    VPN Gateway
       |
       ↓
    Internet

Important:

> VPN encryption protects the traffic across the VPN tunnel. It does not automatically make all Internet activity anonymous or safe.


### Why VPN is Used

VPNs can be used for secure remote access and for protecting traffic across networks that cannot be fully trusted.

Example:

An employee works from home and needs access to company resources.

Without VPN:

    Employee Laptop
          |
          ↓
       Internet
          |
          ↓
    Company Network

With VPN:

    Employee Laptop
          |
          | Encrypted VPN Tunnel
          ↓
    Company VPN Gateway
          |
          ↓
    Company Network
          |
          ├── File Server
          ├── Internal Application
          └── Other Resources

VPNs can therefore provide a protected connection between remote users and a network.


### VPN vs Firewall vs NAT

| Technology | Main Purpose |
|------------|--------------|
| Firewall | Controls network traffic |
| NAT | Translates IP addresses and commonly ports |
| VPN | Creates a protected encrypted tunnel |

Easy memory:

    Firewall → Controls traffic

    NAT → Translates addresses

    VPN → Protects traffic through an encrypted tunnel


---

## 4. How They Work Together

A simplified company network can look like this:

    INTERNET
        |
        | Public Network
        |
        ↓
    ┌─────────────┐
    │  FIREWALL   │
    │ ALLOW/DENY  │
    └──────┬──────┘
           |
          NAT
           |
           ↓
    ┌──────────────────┐
    │ INTERNAL NETWORK │
    │   10.0.0.0/24    │
    └────────┬─────────┘
             |
       ┌─────┼─────┐
       |     |     |
       ↓     ↓     ↓
    Laptop Server Printer
    10.0.0.10 10.0.0.20 10.0.0.30

The firewall controls whether traffic is allowed.

NAT translates between private and public addressing.

The internal network contains devices such as laptops, servers and printers using private IP addresses.

Example outbound traffic:

    Employee Laptop
    10.0.0.10
         |
         | HTTPS
         ↓
      Firewall
         |
         | ALLOW
         ↓
        NAT
         |
         ↓
    Public IP
         |
         ↓
      Internet


---

## 5. SOC Analyst Perspective

A SOC analyst may investigate network and firewall logs to understand what communication occurred.

Common log information includes:

    Timestamp
    Source IP
    Source Port
    Destination IP
    Destination Port
    Protocol
    Action
    Direction
    Bytes

The analyst uses this information together with other logs and context to determine whether traffic is expected or suspicious.


### Internal → External

Internal-to-external traffic means:

    Internal system
          ↓
       Internet

Example:

    SRC=10.0.0.15
    DST=142.250.x.x
    SPORT=52344
    DPORT=443
    PROTO=TCP
    ACTION=ALLOW

This means an internal system made a TCP connection to an external destination on port 443.

A SOC analyst may investigate:

- Which device owns 10.0.0.15?
- Which application created the connection?
- What is the destination?
- Is the destination expected?
- How frequently is the connection happening?
- Did the device show other suspicious activity?


### External → Internal

External-to-internal traffic means:

    Internet
       ↓
    Internal system

Example:

    SRC=185.x.x.x
    DST=10.0.0.20
    DPORT=3389
    PROTO=TCP
    ACTION=DENY

Port 3389 is commonly associated with RDP.

The firewall blocked the connection.

A SOC analyst may investigate:

- Source IP
- Target system
- Number of attempts
- Time of attempts
- Whether the same source targeted multiple systems
- Whether the activity resembles scanning or repeated connection attempts

A blocked event is still useful evidence because it shows that an attempted connection occurred.


### Internal → Internal

Internal-to-internal traffic occurs between systems inside the company network.

Example:

    SRC=10.0.0.10
    DST=10.0.0.20
    DPORT=445
    PROTO=TCP
    ACTION=ALLOW

Port 445 is commonly associated with SMB.

This may be normal in a Windows environment.

However, a pattern such as:

    10.0.0.10 → 10.0.0.20:445
    10.0.0.10 → 10.0.0.21:445
    10.0.0.10 → 10.0.0.22:445
    10.0.0.10 → 10.0.0.23:445
    10.0.0.10 → 10.0.0.24:445

could require investigation because one system is contacting many systems.

The SOC analyst should not automatically assume that internal traffic is safe or external traffic is malicious.

Context and traffic patterns are important.


### NAT Logs

NAT can make investigation more complicated because many internal devices may share one public IP address.

Example:

    Public IP:
    203.0.113.50

Several internal devices may use it:

    10.0.0.10
    10.0.0.11
    10.0.0.12

Suppose an external system sees:

    203.0.113.50:41001

The SOC analyst may need NAT translation information to identify the internal device.

Example:

    203.0.113.50:41001
             ↓
    10.0.0.10:52000

This maps the public connection to the internal system.

NAT logs can therefore be important during security investigations.


### VPN Logs

VPN systems can generate logs containing information such as:

    Username
    Source IP
    VPN-assigned IP
    Login time
    Logout time
    Authentication result

Example:

    USER=vignik
    SRC_IP=49.x.x.x
    VPN_IP=10.20.30.15
    ACTION=LOGIN_SUCCESS
    TIME=09:15

A SOC analyst can correlate VPN logs with other security logs.

Example:

    09:15
    VPN login successful
           ↓
    10.20.30.15 assigned
           ↓
    09:18
    Internal server accessed
           ↓
    09:25
    Large amount of data transferred

This creates a timeline that can help the analyst understand what happened.


---

## 6. Written Task

### Why does a company use both a firewall and NAT?

A company uses both a firewall and NAT because they solve different networking problems. A firewall is mainly used to control and filter network traffic, while NAT is used to translate IP addresses and commonly port information between private and public networks.

A company may have many devices such as laptops, servers, printers and other systems. These devices can use private IP addresses inside the internal network. For example, a laptop may use 10.0.0.10 and a server may use 10.0.0.20. These private addresses are used within the internal network and are not directly used as globally routable Internet addresses.

When internal devices need to communicate with the Internet, NAT can translate their private addressing information to a public IP address. For example, several internal devices can use a public IP such as 203.0.113.50 for Internet connectivity. This is useful because IPv4 addresses are limited and many private devices can share public IPv4 connectivity.

The firewall has a different purpose. It controls which network traffic should be allowed or denied. It can examine information such as source IP, destination IP, ports and protocols. For example, a company may allow internal users to access HTTPS websites using port 443 while blocking unwanted inbound connections to internal systems.

The firewall can control both inbound and outbound traffic. Inbound traffic comes from outside the network toward internal systems. Outbound traffic goes from internal systems toward external destinations. Outbound monitoring is also important because a compromised computer may attempt to communicate with an external command-and-control server or transfer data outside the company.

NAT and firewall functions are often provided by the same network device, but they are still different functions. NAT translates addresses, while the firewall applies security rules to network traffic. NAT should therefore not be considered a replacement for a firewall.

From a SOC analyst's perspective, both technologies provide useful information. Firewall logs can show source IP, destination IP, ports, protocols, timestamps and whether traffic was allowed or denied. NAT logs can help analysts map a public IP and port back to the internal device that generated the connection.

For example, if many internal computers share one public IP, a SOC analyst may need NAT translation logs to determine which internal computer made a particular connection. Therefore, companies use firewalls and NAT together because they provide different functions: the firewall provides traffic control and security filtering, while NAT provides address translation and enables private networks to communicate using public IPv4 connectivity.


### Q1 — Internal Traffic

A SOC analyst may see internal traffic between private IP addresses.

Example:

    SRC=10.0.0.15
    DST=10.0.0.20
    DPORT=445
    PROTO=TCP
    ACTION=ALLOW

This shows that the internal system 10.0.0.15 communicated with 10.0.0.20 using TCP port 445.

The analyst may investigate:

- Which users or devices own the IP addresses?
- Is this communication expected?
- What application created the connection?
- How frequently is it occurring?
- Is one machine communicating with many other systems?
- Are there other suspicious events involving the same device?

Internal traffic is not automatically safe. The analyst needs to understand the normal behavior of the environment and investigate unusual patterns.


### Q2 — External Traffic

A SOC analyst may see traffic between an external IP address and an internal system.

Example:

    SRC=185.x.x.x
    DST=10.0.0.20
    DPORT=3389
    PROTO=TCP
    ACTION=DENY

Port 3389 is commonly associated with RDP.

The firewall denied the connection, but the event is still useful because it shows that an external system attempted to connect to an internal system.

If the same source repeatedly attempts connections to many internal systems, the analyst may investigate whether the activity resembles scanning or repeated unauthorized connection attempts.

The analyst may examine:

- Source IP
- Target IP
- Target port
- Number of attempts
- Time and frequency
- Whether multiple internal systems were targeted
- Related firewall and endpoint logs

The important point is that the SOC analyst looks at the complete pattern and context rather than deciding that a single connection is automatically malicious.


---

## 7. Day 5 Self-Test

### Q1. What is a firewall?

A firewall is a network security control that monitors and controls network traffic according to predefined rules. It can allow, deny or drop traffic.


### Q2. What is inbound traffic?

Inbound traffic is traffic entering a network or system.

Example:

    Internet → Company Server


### Q3. What is outbound traffic?

Outbound traffic is traffic leaving a network or system.

Example:

    Employee Laptop → Internet


### Q4. Why should a SOC monitor outbound traffic?

Because a compromised system may communicate with an attacker's server, download additional malware, receive commands or send data outside the organization.


### Q5. What information can a firewall rule use?

A firewall rule can use information such as:

- Source IP
- Destination IP
- Source port
- Destination port
- Protocol
- Connection state
- Direction

The rule then determines an action such as ALLOW or DENY.


### Q6. What is a stateful firewall?

A stateful firewall tracks the state of active network connections and can determine whether packets belong to an existing connection.


### Q7. What is a stateless firewall?

A stateless firewall evaluates packets individually against configured rules without maintaining connection state in the same way as a stateful firewall.


### Q8. What is the main difference between stateful and stateless?

Stateful firewalls track connection state, while stateless firewalls evaluate packets individually based mainly on configured rules.


### Q9. What does NAT stand for?

NAT stands for:

    Network Address Translation


### Q10. What is a private IP?

A private IP is an IP address used within private networks.

Common private IPv4 ranges include:

    10.0.0.0/8
    172.16.0.0/12
    192.168.0.0/16

Examples:

    10.0.0.10
    172.16.5.20
    192.168.1.50


### Q11. What is a public IP?

A public IP is a globally routable IP address used for communication across the public Internet.

Example:

    203.0.113.50


### Q12. Why is NAT useful for IPv4?

NAT allows many devices using private IPv4 addresses to share public IPv4 connectivity. This helps conserve the limited supply of public IPv4 addresses.


### Q13. What happens here?

    192.168.1.10
          ↓
         NAT
          ↓
    203.0.113.50

The NAT device translates the private source address into a public address for Internet communication. It also keeps translation information so return traffic can be associated with the correct internal connection.


### Q14. Why isn't NAT the same as a firewall?

NAT performs address and commonly port translation, while a firewall controls traffic using security rules. NAT itself is not a replacement for a firewall.


### Q15. What does VPN stand for?

VPN stands for:

    Virtual Private Network


### Q16. What is an encrypted tunnel?

An encrypted tunnel is a protected communication path in which traffic is encrypted between the VPN client/device and the VPN endpoint.


### Q17. What does a VPN protect?

A VPN protects traffic travelling through the VPN tunnel between the device and VPN endpoint using encryption.


### Q18. Does a VPN automatically make someone completely anonymous?

No.

A VPN provides an encrypted connection to the VPN endpoint, but it does not guarantee complete anonymity or complete security. Websites can still identify users through accounts, cookies and other application-level information.


### Q19. Decode this:

    SRC=10.0.0.15
    DST=142.250.x.x
    SPORT=52100
    DPORT=443
    PROTO=TCP
    ACTION=ALLOW

Answer:

    Source:
    10.0.0.15

    Destination:
    142.250.x.x

    Source Port:
    52100

    Destination Port:
    443

    Protocol:
    TCP

    Direction:
    Internal → External

    Action:
    ALLOW

Port 443 is commonly used for HTTPS.


### Q20. Decode this:

    SRC=185.x.x.x
    DST=10.0.0.20
    DPORT=3389
    PROTO=TCP
    ACTION=DENY

Answer:

    Source:
    185.x.x.x

    Destination:
    10.0.0.20

    Destination Port:
    3389

    Protocol:
    TCP

    Direction:
    External → Internal

    Action:
    DENY

Port 3389 is commonly associated with RDP.

The interesting part is that an external system attempted to connect to an internal system. The firewall denied the connection. If the same source repeatedly attempts connections or targets many systems, the SOC analyst may investigate the activity further.

---

# Day 5 Key Takeaways

    Firewall
    = Controls network traffic

    Inbound
    = Outside → Inside

    Outbound
    = Inside → Outside

    Stateful
    = Tracks connections

    Stateless
    = Evaluates packets individually

    NAT
    = Network Address Translation

    Private IP
    = Used inside private networks

    Public IP
    = Used for Internet connectivity

    VPN
    = Virtual Private Network

    VPN Tunnel
    = Protected/encrypted connection between device and VPN endpoint

    SOC
    = Analyze source, destination, ports, protocols,
      timestamps, actions and traffic patterns