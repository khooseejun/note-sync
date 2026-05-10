### OSI Model (from 7 to 1)

| Layer        | PDU     | Usage                                                                |
| ------------ | ------- | -------------------------------------------------------------------- |
| Application  | Data    | process to process communication                                     |
| Presentation | Data    | represent of data compatible between source and destination          |
| Session      | Data    | manage data exchange                                                 |
| Transport    | Segment | segmentation, transfer and reassembly data between end device        |
| Network      | Packet  | provide service to exchange individual pieces of data across network |
| Data Link    | Frame   | methods for exchanging data frames over common media                 |
| Physical     | Bits    | activate and maintain the physical connections for bit transmission  |

---
# Comprehensive Networking Notes (Chapters 1-10)

## 1. Introduction to Networks (Chapter 1)

### Network Components
- **Hosts/End Devices**: Where messages originate or are received (e.g., servers, clients).
- **Intermediary Devices**: Interconnect end devices (e.g., switches, routers, firewalls). They manage data flow, regenerate signals, and notify of errors.
- **Network Media**: The channel for message travel.
    - **Copper**: Electrical impulses.
    - **Fiber-optic**: Pulses of light.
    - **Wireless**: Electromagnetic waves.

### Topology Diagrams
- **Physical Topology**: Physical location of devices and cabling.
- **Logical Topology**: Devices, ports, and addressing scheme.

### Network Types
- **LAN (Local Area Network)**: Small geographical area, high speed, administered by a single organization.
- **WAN (Wide Area Network)**: Wide geographical area, interconnects LANs, typically administered by service providers.
- **Internet**: Worldwide collection of interconnected LANs and WANs.
- **Intranet**: Private collection of LANs/WANs internal to an organization.
- **Extranet**: Provides secure access to an organization's network for external users.

### Reliable Networks (4 Characteristics)
1.  **Fault Tolerance**: Ability to continue operating during a failure.
2.  **Scalability**: Ability to expand quickly without impacting performance.
3.  **Quality of Service (QoS)**: Mechanism to ensure reliable delivery (e.g., prioritizing voice/video).
4.  **Security**: Protecting network infrastructure and data (confidentiality, integrity, availability).

### Network Trends
- **BYOD (Bring Your Own Device)**: Allows users to use personal devices.
- **Cloud Computing**:
    - **Public**: Available to the general public (pay-per-use or free).
    - **Private**: Intended for a specific organization.
    - **Hybrid**: Combination of two or more cloud types.
    - **Custom**: Built for a specific industry.
- **Online Collaboration & Video Communication**.

---

## 2. Protocols and Models (Chapter 2)

### Rules of Communication (Protocols)
Protocols must account for:
- Message encoding, formatting, and encapsulation.
- Message size and timing (flow control, response timeout, access method).
- Message delivery options.

### Message Delivery Options
- **Unicast**: One-to-one communication.
- **Multicast**: One-to-many (not all).
- **Broadcast**: One-to-all (IPv4 only; not in IPv6).

### Protocol Suites (TCP/IP Model)

| TCP/IP Layer | Description |
| :--- | :--- |
| **Application** | Represents data, encoding, dialog control. |
| **Transport** | Supports communication between devices. |
| **Internet** | Determines the best path through the network. |
| **Network Access** | Controls hardware devices and media. |

### Data Encapsulation & PDUs
- **Segmenting**: Breaking messages into smaller units. Benefits: Increases speed and efficiency.
- **Sequencing**: Numbering segments for reassembly (handled by TCP).
- **PDUs (Protocol Data Units)**:
    1.  **Data** (Data Stream)
    2.  **Segment** (Transport Layer - TCP/UDP)
    3.  **Packet** (Network Layer - IP)
    4.  **Frame** (Data Link Layer)
    5.  **Bits** (Bit Stream - Physical Layer)

### Addressing
- **Layer 3 (Logical/IP)**: Delivers packet from original source to final destination. Uses network/host portions.
- **Layer 2 (Physical/MAC)**: Delivers frame from one NIC to another on the **same network**. Changes at each hop.

---

## 3. Physical Layer (Chapter 3)

### Bandwidth Terminology
- **Bandwidth**: Capacity of a medium.
- **Latency**: Time for data to travel from one point to another.
- **Throughput**: Actual bit transfer measure.
- **Goodput**: Usable data transferred (Throughput - overhead).

### Copper Cabling
- **UTP (Unshielded Twisted-Pair)**: Most common. Uses RJ-45. Relies on cancellation and varying twist lengths to limit crosstalk.
- **STP (Shielded Twisted-Pair)**: Better noise protection, uses shielding.
- **Coaxial**: Used for wireless installations and cable internet.
- **Cable Types**:
    - **Straight-through**: Host to Network Device.
    - **Crossover**: Host-to-Host, Switch-to-Switch (legacy due to Auto-MDIX).
    - **Rollover**: Cisco proprietary (host serial port to Router/Switch Console).

### Fiber-Optic Cabling
- **Advantages**: Longer distances, higher bandwidth, immune to EMI/RFI.
- **SMF (Single-mode)**: Very small core, lasers, long-distance.
- **MMF (Multi-mode)**: Larger core, LEDs, up to 550 meters.
- **Connectors**: ST, SC, LC.

### Wireless Media
- **Limitations**: Coverage area, interference, security, shared medium (half-duplex).
- **Standards**: Wi-Fi (802.11), Bluetooth (802.15), WiMAX (802.16), Zigbee (802.15.4).
- **Components**: Wireless Access Point (AP), Wireless NIC adapters.

---

## 4. Data Link Layer (Chapter 4)

### Purpose
- Responsible for communication between end-device NICs.
- Allows upper layers to access the physical layer.
- Encapsulates Layer 3 packets into Layer 2 Frames.
- Performs error detection.

### Topologies
- **WAN Topologies**: Point-to-point, Hub and Spoke, Mesh.
- **LAN Topologies**: Star, Extended Star, Bus, Ring.

### Media Access Control
- **Contention-based**: Nodes compete for medium (half-duplex).
    - **CSMA/CD**: Legacy Ethernet. Transmit, detect collision, wait random time, retransmit.
    - **CSMA/CA**: WLAN. Avoids collisions by including time duration in transmission.
- **Controlled Access**: Deterministic, each node has its own time (e.g., Token Ring).

### Data Link Frame Fields
| Field | Description |
| :--- | :--- |
| **Frame Start/Stop** | Identifies beginning and end of frame. |
| **Addressing** | Indicates source/destination nodes (local delivery). |
| **Type** | Identifies encapsulated Layer 3 protocol. |
| **Data** | Contains the frame payload. |
| **Error Detection** | Determines transmission errors (FCS). |

---

## 5. Ethernet (Chapter 5)

### Sublayers
- **LLC (802.2)**: Identifies which network layer protocol is used.
- **MAC (802.3)**: Responsible for data encapsulation and media access control.

### Ethernet Frame
- **Size**: Minimum 64 bytes, Maximum 1518 bytes (Preamble not included).
- **Key Fields**: Destination MAC, Source MAC, Length/Type, Data (46-1500 bytes), FCS.

### MAC Addresses
- 48-bit binary value expressed as 12 hexadecimal digits.
- **Unicast**: Unique address for single device.
- **Broadcast**: `FF-FF-FF-FF-FF-FF` (IPv4 broadcast).
- **Multicast**: Begins with `01-00-5E` (for IPv4 multicast groups).

### LAN Switches
- **Learning**: Examines source MAC address; adds to MAC address table with port number.
- **Forwarding**: Examines destination MAC; if found, forwards out specific port; if unknown (unknown unicast), floods out all ports except incoming.
- **Filtering**: Forwards frame out a single port if destination MAC is in table.
- **Forwarding Methods**:
    - **Store-and-forward**: Receives entire frame, checks CRC, then forwards.
    - **Cut-through**: Forwards after reading destination MAC (no error checking).
        - *Fast-forward*: Forwards after reading destination address (lowest latency).
        - *Fragment-free*: Stores first 64 bytes before forwarding.

### Address Resolution Protocol (ARP)
- **Purpose**: Resolves IPv4 addresses to MAC addresses on a local network.
- **ARP Request**: Broadcast frame sent when a MAC address is unknown.
- **ARP Reply**: Unicast frame containing the MAC address.
- **Remote Communication**: If destination is on a remote network, the source uses ARP to find the MAC address of its **default gateway**.
- **ARP Table**: Show with `arp -a` (Windows) or `show ip arp` (Cisco). Entries timeout after a period.

---

## 6. IPv4 Addressing (Chapter 6)

### Address Structure
- 32-bit hierarchical address: **Network portion** + **Host portion**.
- **Subnet Mask**: Determines network/host portions (1 = network bit).
- **Prefix Length**: Number of bits set to 1 in the subnet mask (e.g., `/24` = `255.255.255.0`).

### Address Types
- **Network Address**: Represents the network itself (all host bits 0).
- **Broadcast Address**: Used to send to all hosts on the network (all host bits 1).
- **Public Addresses**: Globally unique and routable on the internet.
- **Private Addresses (RFC 1918)**:
    - 10.0.0.0/8 (10.0.0.0 - 10.255.255.255)
    - 172.16.0.0/12 (172.16.0.0 - 172.31.255.255)
    - 192.168.0.0/16 (192.168.0.0 - 192.168.255.255)
- **Special Use**:
    - **Loopback**: `127.0.0.0/8` (commonly `127.0.0.1`) – tests TCP/IP stack.
    - **Link-Local (APIPA)**: `169.254.0.0/16` – self-assigned when no DHCP server.

### Subnetting
- **Purpose**: Reduce broadcast domains, improve security, manage traffic.
- **FLSM (Fixed Length Subnet Mask)**: All subnets have the same mask.
- **VLSM (Variable Length Subnet Mask)**: Allows subnets to have different masks, minimizing wasted addresses.
- **Calculation Formulas**:
    - Number of Subnets = `2^n` (where `n` = borrowed bits)
    - Number of Hosts per Subnet = `2^h - 2` (where `h` = host bits remaining)
- **Magic Number**: The value (place value) of the last `1` in the subnet mask. Add this to the previous subnet address to find the next one.

### Structured Design
- **Gateway (Router)**: `.1` or `.254`
- **Servers/Printers**: Static IPs in a predictable range (e.g., `.230-.249`).
- **Clients**: DHCP assigned.

---

## 7. IPv6 Addressing (Chapter 7)

### IPv4 Issues & IPv6 Advantages
- **Depletion of IPv4**.
- **Issues with NAT** (breaks end-to-end connectivity).
- **IPv6 Advantages**:
    - Larger 128-bit address space.
    - Simplified header for efficient handling.
    - No need for NAT.
    - Autoconfiguration (SLAAC).

### Migration Techniques
1.  **Dual Stack**: Devices run both IPv4 and IPv6 stacks simultaneously.
2.  **Tunneling**: Encapsulating IPv6 packets inside IPv4 packets.
3.  **Translation (NAT64)**: Translating between IPv6 and IPv4 packets.

### Address Representation
- 128 bits, written as 8 hextets of 4 hexadecimal digits.
- **Rule 1 (Omit Leading Zeros)**: `01ab` -> `1ab`.
- **Rule 2 (Double Colon ::)**: Replace a single contiguous string of all-zero hextets with `::` (can only be used once).
    - *Example*: `2001:0db8:0000:1111:0000:0000:0000:0200` -> `2001:db8:0:1111::200`

### Address Types
- **Unicast**:
    - **GUA (Global Unicast)**: Routable on IPv6 internet. Prefix `2000::/3`. Structure: Global Routing Prefix (typically /48) + Subnet ID (usually /64) + Interface ID (64 bits).
    - **LLA (Link-Local)**: Confined to a single link. Prefix `fe80::/10`. Used for routing updates and as default gateway. Automatically generated or manually configured.
    - **Unique Local (ULA)**: Similar to private IPv4 (`fc00::/7`).
- **Multicast**: Prefix `ff00::/8`. No broadcast.
    - **Well-known**: `ff02::1` (all nodes), `ff02::2` (all routers).
- **Anycast**: Multiple devices share the same address.

### Subnetting IPv6
- Subnetting is done using the **Subnet ID** field (typically by borrowing bits from the 64-bit Interface ID space).
- **Recommended prefix length** for LANs: `/64`.

---

## 8. & 9. Transport Layer (Chapter 9) & Network Layer (Chapter 8 combined)

### Comparison of IP Characteristics (Network Layer)

| Characteristic | IPv4 | IPv6 |
| :--- | :--- | :--- |
| **Connectionless** | Yes | Yes |
| **Best Effort (Unreliable)** | Yes | Yes |
| **Media Independent** | Yes | Yes |
| **Address Size** | 32-bit | 128-bit |
| **Fragmentation** | Routers and hosts | Only source host |
| **Header Complexity** | More complex | Simplified |

### TCP vs. UDP (Transport Layer)

| Feature | TCP (Transmission Control Protocol) | UDP (User Datagram Protocol) |
| :--- | :--- | :--- |
| **Connection** | Connection-oriented (3-way handshake) | Connectionless |
| **Reliability** | High (acknowledgments, retransmission) | Low (best-effort) |
| **Sequencing** | Yes (sequence numbers) | No |
| **Flow Control** | Yes (window size) | No |
| **Header Size** | 20-60 bytes | 8 bytes |
| **Typical Uses** | Web (HTTP), Email (SMTP), File (FTP) | Live video, VoIP, DNS, DHCP |
| **Key Analogy** | Registered mail (tracked, acknowledged) | Regular mail (sent, no confirmation) |

### TCP Communication Process
- **Three-Way Handshake (Establish Session)**:
    1.  Client sends **SYN** (synchronize).
    2.  Server replies with **SYN-ACK** (synchronize-acknowledge).
    3.  Client sends **ACK** (acknowledge).
- **Session Termination**:
    1.  Client sends **FIN** (finish).
    2.  Server sends **ACK**.
    3.  Server sends **FIN**.
    4.  Client sends **ACK**.

---

## 10. Application Layer (Chapter 10)

### Common Protocols

| Protocol | Port(s) | Transport | Description |
| :--- | :--- | :--- | :--- |
| **HTTP** | 80 | TCP | Web page transfer (insecure). |
| **HTTPS** | 443 | TCP | Secure web page transfer (HTTP + SSL/TLS). |
| **SMTP** | 25 | TCP | Sending email. |
| **POP3** | 110 | TCP | Receiving email (downloads and deletes from server). |
| **IMAP** | 143 | TCP | Receiving email (keeps copy on server, synchronizes changes). |
| **DNS** | 53 | UDP/TCP | Resolves domain names to IP addresses. |
| **DHCP** | 67 (server), 68 (client) | UDP | Dynamically assigns IP addressing information. |
| **FTP** | 20 (data), 21 (control) | TCP | File transfer. Uses two connections. |
| **SMB** | 445 | TCP | File sharing (Windows). |
| **TFTP** | 69 | UDP | Simple file transfer (no authentication). |

### DNS (Domain Name System)
- **Purpose**: Translate domain names (e.g., `www.cisco.com`) into IP addresses.
- **Hierarchy**: Root -> Top-Level Domain (TLD, e.g., `.com`) -> Second-Level (e.g., `cisco.com`).
- **Record Types**: `A` (IPv4), `AAAA` (IPv6), `NS` (Name Server), `MX` (Mail Exchange).
- **Command**: `nslookup` (query DNS servers).

### DHCP (Dynamic Host Configuration Protocol) - DORA Process
1.  **D**iscover (DHCPDISCOVER): Client broadcasts to find a DHCP server.
2.  **O**ffer (DHCPOFFER): Server responds with an IP address lease offer.
3.  **R**equest (DHCPREQUEST): Client requests the offered address.
4.  **A**cknowledge (DHCPACK): Server acknowledges and finalizes the lease.