# Cisco Packet Tracer Test - Network Configuration Guide

Based on the provided PDF and topology diagram, here is a comprehensive step-by-step guide to complete this network configuration lab.

---

## Understanding the Topology

### TAR UMT Hostel Network
- **Wireless Router0**: 192.168.5.1/24
- **HostelAdminPC**: 192.168.5.10/24
- **Laptop0, Smartphone0, TabletPC0**: DHCP (Wireless clients)

### ABC Company Network
- **LAN_A1**: 172.20.0.0/16 (Router1 G0/0)
- **LAN_B2**: 192.168.8.128/25 (Router2 G0/0)
- **Router1**: G0/0 = 172.20.0.1/16, S0/0/0 = 10.1.1.1/30
- **Router2**: G0/0 = 192.168.8.129/25, S0/0/0 = 10.1.1.2/30
- **AdminPC**: 172.20.0.10/16 (Gateway: 172.20.0.1)
- **PC1, PC2, PC3**: DHCP (in LAN_B2)
- **Servers**: 172.20.0.100/16 (NTP, DNS, Web, TFTP)

---

## Part 1: Configure HostelAdminPC

1. Click on **HostelAdminPC** → **Desktop** → **IP Configuration**
2. Set:
   - **IP Address**: 192.168.5.10
   - **Subnet Mask**: 255.255.255.0
   - **Default Gateway**: 192.168.5.1

---

## Part 2: Configure Wireless Router0

### Step 2a: Access Web Interface
1. On **HostelAdminPC** → **Desktop** → **Web Browser**
2. Enter: `192.168.5.1`
3. Login with:
   - **Username**: admin
   - **Password**: admin

### Step 2d: DHCP Settings
1. Navigate to **DHCP** settings
2. Verify **Internal Network**: 192.168.5.0/24
3. Set **Start IP Address**: 20
4. Set **Maximum Number of Users**: 200

### Step 2e-g: Wireless Settings (2.4 GHz)
1. Navigate to **Wireless** → **Basic Wireless Settings**
2. **Network Mode**: Mixed
3. **Network Name (SSID)**: HostelBlockA
4. **Standard Channel**: 6 - 2.437GHz
5. **Disable 5 GHz frequencies** (both radios)
6. Click **Save Settings**

### Step 2h: Security Settings
1. Navigate to **Wireless** → **Wireless Security**
2. **Security Mode**: WPA2 Personal
3. **Encryption**: AES
4. **Passphrase**: TARUMT2025SS
5. Click **Save Settings**

---

## Part 3: Connect Wireless Devices

### Step 3a: Connect to Wireless Network
For each device (**Laptop0**, **Smartphone0**, **TabletPC0**):

1. Click on device → **Desktop** → **PC Wireless** (or equivalent)
2. Select **HostelBlockA** network
3. Enter passphrase: **TARUMT2025SS**
4. Connect and obtain DHCP IP address

### Step 3b: Verify Connectivity
- Open **Command Prompt** on each wireless device
- Ping the default gateway:
  ```
  ping 192.168.5.1
  ```
- Ping other wireless devices to verify connectivity

---

## Part 4: Configure AdminPC

1. Click on **AdminPC** → **Desktop** → **IP Configuration**
2. Set:
   - **IP Address**: 172.20.0.10
   - **Subnet Mask**: 255.255.0.0
   - **Default Gateway**: 172.20.0.1
   - **DNS Server**: 172.20.0.100

---

## Part 5: Configure Basic Security on Router1

### Step 5a: Console into Router1
1. On **AdminPC** → **Desktop** → **Terminal**
2. Click **OK** (to console into Router1)

### Step 5b: Set Hostname
```
enable
configure terminal
hostname Router1
```

### Step 5c: Configure Interfaces
```
interface g0/0
ip address 172.20.0.1 255.255.0.0
no shutdown
exit

interface s0/0/0
ip address 10.1.1.1 255.255.255.252
no shutdown
exit
```

### Step 5d: Encrypt Passwords
```
service password-encryption
```

### Step 5e: Set Secret Password
```
enable secret ABC_love123@
```

### Step 5f: Disable DNS Lookup
```
no ip domain-lookup
```

---

## Part 6: Configure SSH on Router1

### Step 6a: Set Domain Name
```
ip domain-name FOCS.com
```

### Step 6b: Create Administrator User
```
username administrator secret ABC456SS
```

### Step 6c: Generate RSA Keys
```
crypto key generate rsa
```
- When prompted: **1024** (key length)

### Step 6d: Configure Login Blocking
```
login block-for 180 attempts 5 within 120
```
(180 seconds = 3 minutes, 120 seconds = 2 minutes)

### Step 6e-f: Configure VTY Lines
```
line vty 0 4
transport input ssh
login local
exec-timeout 5 0
exit
```

### Step 6g: Save Configuration
```
copy running-config startup-config
```
Press **Enter** to confirm

### Step 6h: Verify SSH Connection
1. On **PC1** → **Desktop** → **Command Prompt**
2. Type:
   ```
   ssh -l administrator 10.1.1.1
   ```
3. Enter password: **ABC456SS**
4. You should see the Router1 prompt

---

## Part 7: Configure NTP on Router1

### Step 7a-b: Configure as NTP Client
```
configure terminal
ntp server 172.20.0.100
exit
show ntp status
show clock
```

---

## Part 8: Configure Router1 as DHCP Server

### Step 8a: Exclude First 100 Addresses from LAN_A1
```
ip dhcp excluded-address 172.20.0.1 172.20.0.100
```

### Step 8b: Exclude First 10 Addresses from LAN_B2
```
ip dhcp excluded-address 192.168.8.129 192.168.8.138
```

### Step 8c: Create DHCP Pool for LAN_A1
```
ip dhcp pool LAN_A1
network 172.20.0.0 255.255.0.0
default-router 172.20.0.1
dns-server 172.20.0.100
exit
```

### Step 8d: Create DHCP Pool for LAN_B2
```
ip dhcp pool LAN_B2
network 192.168.8.128 255.255.255.128
default-router 192.168.8.129
dns-server 172.20.0.100
exit
```

### Save Configuration
```
copy running-config startup-config
```

---

## Troubleshooting Tips

### If Wireless Devices Can't Connect:
1. Verify **SSID** is exactly "HostelBlockA" (case sensitive)
2. Check passphrase **TARUMT2025SS** (case sensitive)
3. Ensure 2.4 GHz radio is enabled
4. Press **Fast Forward Time** button

### If Pings Fail:
1. Check IP configurations
2. Verify interfaces are **up/up** (`show ip interface brief`)
3. For Router1-Router2 connectivity: verify both S0/0/0 interfaces are on the same subnet
4. Check default gateways are configured correctly

### For DHCP Issues:
1. Verify DHCP pools are created correctly
2. Check excluded address ranges
3. Verify devices are set to **DHCP** (not static IP)
4. Use `show ip dhcp binding` to see assigned addresses

---

## Quick Command Reference

| Task | Command |
|------|---------|
| Enter privileged mode | `enable` |
| Enter global config | `configure terminal` |
| Save config | `copy running-config startup-config` |
| Show interfaces | `show ip interface brief` |
| Show DHCP bindings | `show ip dhcp binding` |
| Show NTP status | `show ntp status` |
| Show clock | `show clock` |
| SSH from PC | `ssh -l administrator 10.1.1.1` |

---

## Final Verification Checklist

- [ ] HostelAdminPC can access Wireless Router0 web interface
- [ ] Wireless devices obtain DHCP IP addresses in 192.168.5.20-220 range
- [ ] All wireless devices can ping each other and the gateway
- [ ] AdminPC has correct static IP, gateway, and DNS
- [ ] Router1 has correct hostname and interfaces
- [ ] SSH works from PC1 to Router1
- [ ] NTP synchronizes Router1 clock with NTP server
- [ ] DHCP assigns addresses to PC1, PC2, PC3 in LAN_B2