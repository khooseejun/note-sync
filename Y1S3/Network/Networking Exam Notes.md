## 1. LAN & WAN Identification and the "Circle" (Node Icon)

### LAN (Local Area Network)
- Spans a small geographical area (e.g., a home, office, or campus).
- Interconnects end devices (hosts) like computers, printers, servers.
- Administered by a single organization or individual.
- Provides high-speed bandwidth (typically 100 Mbps to 10 Gbps).

### WAN (Wide Area Network)
- Spans a wide geographical area (e.g., cities, countries, continents).
- Interconnects multiple LANs over long distances.
- Typically administered by one or more service providers (SPs).
- Usually provides slower speed links between LANs (e.g., T1, DSL, Metro Ethernet).

### The "Circle" – Node Icon
- In network diagrams, a **circle** (node icon) represents any generic device (host, switch, router, etc.).
- Used to simplify topology drawings when the exact device type is not important.
- Example: In multicast/broadcast illustrations, a circle may represent each receiving device.

![Node Icon Example - circle represents any device](*conceptually, a circle symbol)

---

## 2. Intermediary Devices: Functions and OSI Layers

Intermediary devices interconnect end devices and manage data flow.

| Device | OSI Layer | Primary Functions |
|--------|-----------|--------------------|
| **Switch** | Layer 2 (Data Link) | - Forwards frames based on MAC addresses<br>- Builds and maintains MAC address table<br>- Regenerates and retransmits signals<br>- Provides error checking (store-and-forward) |
| **Router** | Layer 3 (Network) | - Forwards packets based on IP addresses<br>- Determines best path using routing protocols<br>- Connects different networks (LANs and WANs)<br>- Performs packet filtering and security |

### Additional Intermediary Device Functions
- Regenerate and retransmit data signals.
- Maintain information about network pathways.
- Notify other devices of errors and communication failures.
- Manage data collisions (legacy hubs use CSMA/CD; switches eliminate collisions).

---

## 3. Network Media Types and the OSI Layer Used

**All network media operate at Layer 1 – Physical Layer.**

| Media Type | Description | Characteristics | Connectors/Standards |
|------------|-------------|----------------|----------------------|
| **UTP (Unshielded Twisted Pair)** | 4 pairs of copper wires twisted together | - Most common, inexpensive<br>- Susceptible to EMI/RFI<br>- Uses cancellation and varying twists | RJ-45, Cat5e/6, up to 100m |
| **STP (Shielded Twisted Pair)** | Copper wires with foil/braid shielding | - Better noise protection<br>- More expensive, harder to install | RJ-45, requires grounding |
| **Coaxial Cable** | Copper core with insulating layer, braided shield | - Resists EMI<br>- Used for cable internet & wireless antennas | BNC, F-type connectors |
| **Fiber-Optic** | Glass/plastic strands, light pulses | - Very high bandwidth (up to 100 Gbps)<br>- Immune to EMI<br>- Long distances (up to 100 km) | ST, SC, LC connectors; SMF (yellow), MMF (orange/aqua) |
| **Wireless** | Electromagnetic waves (radio, microwave) | - No physical cable<br>- Shared medium, half-duplex<br>- Subject to interference | IEEE 802.11 (Wi-Fi), Bluetooth, WiMAX |

### Which Layer Uses Media?
- **Physical Layer (Layer 1)** – encodes bits into signals (electrical, light, radio) and transmits them over the medium.
- The **Data Link Layer (Layer 2)** decides when to use the medium (media access control) but does not define the physical medium itself.

---

## 4. Switch Forwarding and Learning

### MAC Address Table (CAM Table)
- Dynamically built by examining the **source MAC address** of incoming frames.
- Entries are timestamped and aged out after a default of **5 minutes**.

### Learning Process
1. Switch receives a frame on a port.
2. It reads the **source MAC address**.
3. If unknown, adds entry (MAC + port) to the table.
4. If known, updates the refresh timer for that entry.

### Forwarding/Filtering Decisions

| Destination MAC Type | Switch Action |
|----------------------|----------------|
| **Known unicast** | Forwards frame only out the associated port (filtering) |
| **Unknown unicast** | Floods frame out all ports except the incoming port |
| **Broadcast (FF:FF:FF:FF:FF:FF)** | Floods all ports except incoming |
| **Multicast (01:00:5E...)** | Floods or forwards based on multicast group |

### Forwarding Methods on Cisco Switches

| Method | Description | Latency |
|--------|-------------|---------|
| **Store-and-forward** | Receives entire frame, checks CRC, then forwards | Higher |
| **Cut-through** | Forwards after reading destination MAC (no error check) | Lowest |
| - Fast-forward | Forwards immediately after destination address | Very low |
| - Fragment-free | Stores first 64 bytes (avoids collision fragments) | Medium |

### Memory Buffering
- **Port-based memory**: Frames stored in queues per port.
- **Shared memory**: All frames deposited into a common buffer shared by all ports.

---

## 5. ARP Process – Step by Step

**ARP (Address Resolution Protocol)** maps an IPv4 address to a MAC address on a local network.

### Step-by-Step ARP Process

1. **Host checks its ARP table**  
   - `arp -a` (Windows) or `show ip arp` (Cisco)  
   - If destination IP-to-MAC mapping exists, use it.

2. **ARP Request (Broadcast)**  
   - If no mapping, sender creates an ARP request.  
   - Request contains:  
     - Sender’s IP and MAC  
     - Target IP (destination’s IP)  
     - Target MAC = 00:00:00:00:00:00 (unknown)  
   - Frame destination MAC = **FF:FF:FF:FF:FF:FF** (broadcast).  
   - All devices on the local network receive and process it.

3. **Only the target device responds**  
   - Device with matching target IP sends an **ARP Reply** (unicast directly to sender).  
   - Reply includes its MAC address.

4. **Sender updates ARP table**  
   - Adds the new IP-to-MAC mapping.  
   - Uses that MAC address as the frame’s destination.

5. **Data transmission proceeds**  
   - Encapsulates IP packet in an Ethernet frame with correct destination MAC.

### ARP Table Management
- Entries are **time stamped** and removed after a timer expires (typically 1–5 minutes, OS-dependent).
- Administrators can manually clear entries (`arp -d` or `clear arp-cache`).
- ARP spoofing/poisoning is a security risk (threat actor sends fake ARP replies).

### ARP for Remote Communication
- If destination IP is on a **different network**, host uses ARP to find the **default gateway’s MAC address**.
- The gateway (router) then forwards the packet toward the remote destination.

---

## 6. OSI Layers and Protocol Data Units (PDUs)

### OSI 7-Layer Model with PDU Names (TCP/IP naming in parentheses)

| OSI Layer | PDU Name (TCP/IP naming) | Description |
|-----------|--------------------------|-------------|
| 7 – Application | **Data** (Data) | User data, protocols like HTTP, FTP, SMTP |
| 6 – Presentation | **Data** (Data) | Data translation, encryption, compression |
| 5 – Session | **Data** (Data) | Session establishment, maintenance, termination |
| 4 – Transport | **Segment** (Segment) | Segmentation, flow control, reliable delivery (TCP) |
| 3 – Network | **Packet** (Packet) | Logical addressing (IP), routing |
| 2 – Data Link | **Frame** (Frame) | Physical addressing (MAC), error detection (FCS) |
| 1 – Physical | **Bits** (Bits) | Raw bit stream over physical medium |

### Encapsulation Process (Top-down)
```
Data (Stream) → Segment → Packet → Frame → Bits
```

### De-encapsulation Process (Bottom-up)
```
Bits → Frame → Packet → Segment → Data (Stream)
```

### Memory Aid
- **Please Do Not Throw Sausage Pizza Away** (Layer 7 to 1)  
- **All People Seem To Need Data Processing** (Layer 1 to 7)

---

## 7. Switch Access Methods: Contention Control – CSMA/CD and CSMA/CA

### Contention-Based Access Methods
Used when multiple devices share the same medium and must compete for transmission time.

| Method | Standard | Operation | Collision Handling |
|--------|----------|-----------|---------------------|
| **CSMA/CD** | IEEE 802.3 (legacy Ethernet with hubs) | Half-duplex; devices listen before sending. If collision occurs, they detect, wait random time, retransmit. | **Collision Detection** |
| **CSMA/CA** | IEEE 802.11 (Wi-Fi) | Half-duplex; devices announce how long they will occupy the medium. Other devices defer. | **Collision Avoidance** |

### CSMA/CD (Carrier Sense Multiple Access / Collision Detection)
- Used on **legacy Ethernet bus topologies** and **hubs**.
- Also occurs if a switch port is misconfigured as half-duplex.
- Steps:
  1. Listen to medium (carrier sense).
  2. If idle, transmit.
  3. If collision detected, send jamming signal.
  4. Wait random backoff time.
  5. Retransmit.

### CSMA/CA (Carrier Sense Multiple Access / Collision Avoidance)
- Used on **wireless LANs (Wi-Fi)**.
- Cannot detect collisions while transmitting (radio half-duplex).
- Steps:
  1. Listen for medium to be idle.
  2. Wait random short period.
  3. Send **RTS (Request to Send)**.
  4. Destination replies with **CTS (Clear to Send)**.
  5. Transmit data, including duration information.
  6. Other devices defer for that duration.

### Modern Ethernet Switches – Full Duplex
- Switches today operate in **full-duplex** mode.
- **No contention** – devices can send and receive simultaneously.
- **CSMA/CD is disabled** in full-duplex.
- Auto-MDIX automatically detects cable type (straight-through or crossover).

---

## 8. Internet, Extranet, and Intranet

| Term | Definition | Access | Example |
|------|------------|--------|---------|
| **Internet** | Worldwide public collection of interconnected LANs and WANs. | Open to anyone (with connection). | Global web, email, social media. |
| **Intranet** | Private network internal to an organization (LANs + WANs). | Only employees or authorized members. | Company internal website, HR portal. |
| **Extranet** | Extension of an intranet that allows secure access to external partners (suppliers, customers, etc.). | Limited, authenticated external users. | Partner portal, vendor supply chain system. |

### Characteristics
- **Internet** – No single owner; governed by IETF, ICANN, IAB.
- **Intranet** – Owned by organization; uses same technologies as internet but firewalled.
- **Extranet** – Uses VPNs or secure tunnels to grant selective access.

---

## 9. Bandwidth, Throughput, and Goodput

These terms describe network performance at the physical and data link layers.

| Term | Definition | Formula / Notes |
|------|------------|------------------|
| **Bandwidth** | Maximum capacity of a medium to carry data (theoretical). | Measured in bps, Kbps, Mbps, Gbps, Tbps. Example: 100 Mbps Ethernet. |
| **Throughput** | Actual measured transfer of bits across the media over a given period. | Always lower than bandwidth due to: traffic load, latency, protocol overhead, collisions. |
| **Goodput** | Usable data transferred (excluding protocol overhead like headers, acknowledgments, retransmissions). | Goodput = Throughput – Overhead. Example: File download speed after TCP/IP headers removed. |

### Units Table

| Unit | Abbreviation | Equivalence |
|------|-------------|-------------|
| Bits per second | bps | 1 bps |
| Kilobits per second | Kbps | 1,000 bps |
| Megabits per second | Mbps | 1,000,000 bps |
| Gigabits per second | Gbps | 1,000,000,000 bps |
| Terabits per second | Tbps | 1,000,000,000,000 bps |

### Key Relationships
- **Bandwidth** = pipe size (capacity)
- **Throughput** = actual water flow (may vary)
- **Goodput** = water that reaches the glass (usable data)

### Factors Affecting Throughput
- Amount of traffic / congestion
- Type of traffic (real-time vs. bulk)
- Latency (delays caused by devices and distance)
- Packet loss and retransmissions

---

## Quick Reference Summary Table

| Topic | Key Points |
|-------|-------------|
| LAN | Small area, high speed, single admin |
| WAN | Wide area, slower, connects LANs |
| Node Icon | Circle representing any network device |
| Switch | Layer 2, forwards frames, learns MAC addresses |
| Router | Layer 3, forwards packets, routes between networks |
| Physical Media | Layer 1 – UTP, STP, Coax, Fiber, Wireless |
| Switch Forwarding | Store-and-forward (CRC) or Cut-through (low latency) |
| ARP | Broadcast request → Unicast reply → Caches mapping |
| OSI PDUs | Data (5-7), Segment (4), Packet (3), Frame (2), Bits (1) |
| CSMA/CD | Half-duplex, collision detection (legacy Ethernet) |
| CSMA/CA | Half-duplex, collision avoidance (Wi-Fi) |
| Full-duplex | No contention, simultaneous send/receive (modern switches) |
| Internet | Public worldwide network |
| Intranet | Private internal network |
| Extranet | Private network with limited external access |
| Bandwidth | Theoretical maximum capacity |
| Throughput | Actual measured transfer rate |
| Goodput | Usable data after overhead |