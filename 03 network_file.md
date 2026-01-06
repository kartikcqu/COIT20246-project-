# Network Design

## 1. Assumptions

### 1.1 Location of Headquarters
**City:** Brisbane, Queensland

The headquarters is located in Brisbane as per the project specification requirement. Brisbane is an ideal location for Truelec's headquarters given its strategic position for accessing major industrial and construction projects across Queensland and Australia.

### 1.2 Branch Office Locations
The following branch office locations have been selected:

1. **Perth** - Western Australia regional office
2. **Adelaide** - South Australia regional office  
3. **Hobart** - Tasmania regional office
4. **Melbourne** - Victoria regional office

These locations provide strategic coverage across major Australian cities where Truelec conducts industrial and construction projects, complementing the Brisbane headquarters.

### 1.3 Headquarters Staff Count
**Total Staff:** 65 employees

Breakdown:
- Project Management Consultants: 15
- Marketing Team: 8
- Senior Leadership: 7
- ICT Staff: 10
- Administrative Support: 15
- Electricians/Engineers (HQ-based): 10

This falls within the specified range of 50-75 staff.

### 1.4 Branch Office Staff Count
**Selected Branch for Design:** Perth  
**Total Staff:** 22 employees

Breakdown:
- Electricians: 12
- Electrical Engineers: 4
- Site Supervisors: 3
- Support Staff: 3

This falls within the specified range of 15-30 staff per branch.

### 1.5 Additional Assumptions

1. **Building Layout:**
   - Headquarters: 3-floor building with approximately 3,000 m² per floor
   - Branch: Single-floor office with approximately 800 m²

2. **Network Usage:**
   - Heavy use of cloud-based CRM, accounting software, HR systems
   - Internal file servers for project documentation
   - Video conferencing capabilities required
   - CCTV and IoT devices for security

3. **Internet Requirements:**
   - Headquarters: 1 Gbps primary connection with 500 Mbps backup
   - Branch: 500 Mbps primary connection with 250 Mbps backup

4. **Redundancy Requirements:**
   - Dual ISP connections at headquarters
   - Dual-core routing at headquarters
   - Backup power supply (UPS) for critical systems

## 2. Network Design

### 2.1 Headquarters Network Design

![Headquarters Network Diagram](diagrams/headquarters-network.png)

#### Design Overview
The headquarters network is designed with redundancy and scalability in mind. The design follows a hierarchical three-layer model:

**Core Layer:**
- Two core routers (Router-Core-1 and Router-Core-2) for redundancy
- Dual ISP connections (ISP-Primary and ISP-Backup)
- Load balancing and automatic failover capability

**Distribution Layer:**
- Three distribution switches per floor (9 total for 3 floors)
- VLAN-capable managed switches for traffic segmentation
- Connection to WiFi access points

**Access Layer:**
- Access switches in departments/zones
- End-user workstations and devices
- IoT devices (CCTV, sensors, RFID readers)

#### Key Design Decisions

**1. Dual Core Routers:**
We chose to implement two core routers instead of one to meet the redundancy requirement specified in the scenario. If one router fails, the second router automatically takes over, ensuring continuous connectivity. The routers are configured with HSRP (Hot Standby Router Protocol) for automatic failover.

**2. Dual ISP Connections:**
Two separate internet connections from different ISPs provide redundancy for WAN connectivity. If the primary ISP fails, traffic automatically routes through the backup ISP. This is critical for a business that relies on cloud services and remote branch connectivity.

**3. Hierarchical Design:**
The three-layer hierarchical design provides:
- Scalability: Easy to add new floors or departments
- Performance: Distribution layer prevents broadcast storms
- Manageability: Clear separation of network functions
- Redundancy: Multiple paths between layers

**4. Separate VLAN for IoT/Security Devices:**
CCTV cameras, IoT sensors, and RFID readers are placed on a separate network segment (VLAN) to isolate them from the main corporate network. This prevents security devices from being compromised if the corporate network is breached, and vice versa.

### 2.2 Branch Office Network Design

![Branch Network Diagram](diagrams/branch-network.png)

#### Design Overview
The branch office uses a simpler two-layer design appropriate for the smaller staff count:

**Core/Distribution Layer:**
- One primary router with backup link
- Two managed switches for redundancy
- VPN connection to headquarters

**Access Layer:**
- Access switches for workstations
- WiFi access points
- Limited IoT devices

#### Key Design Decisions

**1. Simplified Design:**
With only 22 staff, a full three-layer hierarchy is not necessary. The combined core/distribution layer reduces cost while maintaining functionality.

**2. VPN to Headquarters:**
A site-to-site VPN tunnel connects the branch to headquarters, allowing secure access to central servers and shared resources. This is more cost-effective than a dedicated leased line.

**3. Local Internet Breakout:**
Branch office has its own internet connection for local traffic, reducing load on the VPN tunnel. Only corporate traffic (file servers, internal systems) routes through the VPN.

## 3. WiFi Design

### 3.1 WiFi Coverage Requirements

**Headquarters:**
- Coverage across all 3 floors (9,000 m² total)
- Approximately 15 access points total (5 per floor)
- Support for 65 staff plus guest devices

**Branch Office:**
- Coverage across single floor (800 m²)
- Approximately 3 access points
- Support for 22 staff plus guest devices

### 3.2 WiFi Settings and Configuration

| Setting | Value | Justification |
|---------|-------|---------------|
| **Standard** | WiFi 6 (802.11ax) | Latest standard, better performance with multiple devices, improved security |
| **Frequency Bands** | Dual-band (2.4 GHz + 5 GHz) | 5 GHz for high-speed corporate use, 2.4 GHz for IoT devices and extended range |
| **Channel Width** | 80 MHz (5 GHz), 20 MHz (2.4 GHz) | Optimal balance between speed and interference |
| **Security Protocol** | WPA3-Enterprise | Strongest security, individual user authentication |
| **SSID Configuration** | 3 SSIDs: "Truelec-Corporate", "Truelec-Guest", "Truelec-IoT" | Separation of corporate, guest, and IoT traffic |
| **Authentication** | RADIUS server with Active Directory | Centralized authentication, user-specific access control |
| **Guest Network** | Captive portal with time-limited access | Secure guest access without exposing corporate network |
| **Transmit Power** | Auto-adjust (15-20 dBm) | Optimizes coverage without excessive interference |
| **Channel Selection** | Auto (DFS channels enabled) | Reduces interference, maximizes available spectrum |
| **Roaming** | 802.11r (Fast Roaming) enabled | Seamless handoff between access points |
| **QoS** | WMM enabled, prioritize voice/video | Ensures quality for video conferencing |

### 3.3 Access Point Placement

**Headquarters:**
- **Floor 1 (Ground):** 5 APs covering reception, meeting rooms, administrative offices
- **Floor 2:** 5 APs covering project management and marketing departments
- **Floor 3:** 5 APs covering senior leadership and ICT staff areas

**Branch Office:**
- **Main Area:** 2 APs covering office spaces
- **Workshop/Storage:** 1 AP for limited coverage in support areas

### 3.4 WiFi Network Segmentation

| SSID | VLAN | Purpose | Access Level |
|------|------|---------|--------------|
| Truelec-Corporate | VLAN 10 | Corporate staff devices | Full network access |
| Truelec-Guest | VLAN 20 | Visitor/contractor devices | Internet only, no internal access |
| Truelec-IoT | VLAN 30 | CCTV, sensors, RFID | Isolated, access to security server only |

## 4. IP Addressing Scheme

### 4.1 IP Address Requirements
As per project specification, all IP addresses must start with **42** (last two digits of student ID 12304142).

Network masks are restricted to /16 or /24.

### 4.2 Headquarters IP Allocation

| Network Segment | IP Range | Subnet Mask | Available Hosts | Usage |
|-----------------|----------|-------------|-----------------|-------|
| HQ Management Network | 42.10.0.0/24 | 255.255.255.0 | 254 | Core routers, switches, management |
| HQ Floor 1 Staff | 42.10.1.0/24 | 255.255.255.0 | 254 | Workstations, printers (Floor 1) |
| HQ Floor 2 Staff | 42.10.2.0/24 | 255.255.255.0 | 254 | Workstations, printers (Floor 2) |
| HQ Floor 3 Staff | 42.10.3.0/24 | 255.255.255.0 | 254 | Workstations, printers (Floor 3) |
| HQ WiFi Corporate | 42.10.10.0/24 | 255.255.255.0 | 254 | Corporate WiFi devices |
| HQ WiFi Guest | 42.10.20.0/24 | 255.255.255.0 | 254 | Guest WiFi devices |
| HQ IoT/Security | 42.10.30.0/24 | 255.255.255.0 | 254 | CCTV, sensors, RFID |
| HQ Servers | 42.10.100.0/24 | 255.255.255.0 | 254 | File servers, application servers |

**Total IP addresses allocated:** 2,032 (with room for growth)

### 4.3 Branch Office IP Allocation

| Network Segment | IP Range | Subnet Mask | Available Hosts | Usage |
|-----------------|----------|-------------|-----------------|-------|
| Perth Branch Management | 42.20.0.0/24 | 255.255.255.0 | 254 | Router, switches, management |
| Perth Branch Staff | 42.20.1.0/24 | 255.255.255.0 | 254 | Workstations, printers |
| Perth Branch WiFi | 42.20.10.0/24 | 255.255.255.0 | 254 | WiFi devices |
| Perth Branch IoT | 42.20.30.0/24 | 255.255.255.0 | 254 | Security devices |

### 4.4 WAN IP Allocation

| Connection | IP Range | Usage |
|------------|----------|-------|
| HQ to Perth VPN | 42.100.1.0/24 | Site-to-site VPN tunnel |
| HQ to Adelaide VPN | 42.100.2.0/24 | Site-to-site VPN tunnel |
| HQ to Hobart VPN | 42.100.3.0/24 | Site-to-site VPN tunnel |
| HQ to Melbourne VPN | 42.100.4.0/24 | Site-to-site VPN tunnel |

### 4.5 Key IP Address Examples

**Headquarters:**
- Core Router 1: 42.10.0.1
- Core Router 2: 42.10.0.2
- Primary DNS Server: 42.10.100.10
- File Server: 42.10.100.20
- DHCP Server: 42.10.100.30

**Perth Branch:**
- Branch Router: 42.20.0.1
- Main Switch: 42.20.0.10
- Local Server: 42.20.1.100

## 5. Hardware Recommendations

### 5.1 Headquarters Equipment

#### Core Network Equipment

| Equipment | Model/Specification | Quantity | Unit Price (AUD) | Total Price (AUD) | Link |
|-----------|-------------------|----------|------------------|-------------------|------|
| **Core Router** | Cisco ISR 4451 (4-port GE, 2x10GE) | 2 | $8,500 | $17,000 | [Cisco ISR 4451](https://www.cisco.com/c/en/us/products/routers/4000-series-integrated-services-routers-isr/index.html) |
| **Distribution Switch** | Cisco Catalyst 9300-48P (48-port PoE+, 10G uplinks) | 9 | $7,200 | $64,800 | [Catalyst 9300](https://www.cisco.com/c/en/us/products/switches/catalyst-9300-series-switches/index.html) |
| **Access Switch** | Cisco Catalyst 1000-24P (24-port PoE) | 15 | $1,800 | $27,000 | [Catalyst 1000](https://www.cisco.com/c/en/us/products/switches/catalyst-1000-series-switches/index.html) |
| **WiFi Access Point** | Cisco Catalyst 9130AXI (WiFi 6) | 15 | $1,400 | $21,000 | [Catalyst 9130](https://www.cisco.com/c/en/us/products/wireless/catalyst-9130ax-access-points/index.html) |
| **Firewall** | Fortinet FortiGate 200F | 1 | $4,500 | $4,500 | [FortiGate 200F](https://www.fortinet.com/products/next-generation-firewall) |
| **Wireless Controller** | Cisco Catalyst 9800-40 | 1 | $12,000 | $12,000 | [Catalyst 9800](https://www.cisco.com/c/en/us/products/wireless/catalyst-9800-series-wireless-controllers/index.html) |

#### Servers and Storage

| Equipment | Specification | Quantity | Unit Price (AUD) | Total Price (AUD) |
|-----------|--------------|----------|------------------|-------------------|
| **File Server** | Dell PowerEdge R750 (2x Xeon Silver, 128GB RAM, 8TB storage) | 2 | $9,500 | $19,000 |
| **Application Server** | Dell PowerEdge R650 (2x Xeon Silver, 64GB RAM, 4TB storage) | 3 | $7,200 | $21,600 |
| **Backup Storage** | Synology RackStation RS2423+ (12-bay NAS, 48TB) | 1 | $5,800 | $5,800 |

#### Other Equipment

| Equipment | Specification | Quantity | Unit Price (AUD) | Total Price (AUD) |
|-----------|--------------|----------|------------------|-------------------|
| **UPS** | APC Smart-UPS 5000VA Rack | 3 | $3,200 | $9,600 |
| **Cable** | Cat6a Ethernet cable (bulk, 1000m) | 3 boxes | $450 | $1,350 |
| **Patch Panels** | 48-port patch panel | 15 | $180 | $2,700 |
| **Rack Cabinet** | 42U Network Rack | 3 | $1,200 | $3,600 |

**Headquarters Total:** $209,950 AUD

### 5.2 Branch Office Equipment (Perth)

| Equipment | Model/Specification | Quantity | Unit Price (AUD) | Total Price (AUD) |
|-----------|-------------------|----------|------------------|-------------------|
| **Router** | Cisco ISR 4331 (3-port GE) | 1 | $3,800 | $3,800 |
| **Core Switch** | Cisco Catalyst 1000-48P | 2 | $2,400 | $4,800 |
| **WiFi Access Point** | Cisco Catalyst 9120AXI | 3 | $1,200 | $3,600 |
| **Firewall** | Fortinet FortiGate 60F | 1 | $1,800 | $1,800 |
| **Local Server** | Dell PowerEdge T340 Tower | 1 | $4,500 | $4,500 |
| **UPS** | APC Smart-UPS 1500VA | 1 | $950 | $950 |
| **Network Rack** | 24U Network Rack | 1 | $800 | $800 |
| **Cabling & Misc** | Cat6 cables, patch panels | - | - | $1,500 |

**Branch Office Total:** $21,750 AUD

### 5.3 Equipment Justification

**Cisco Networking Equipment:**
- Industry-leading reliability and support
- Proven track record in enterprise environments
- Excellent security features and regular updates
- Compatible across headquarters and branches for easier management

**Power over Ethernet (PoE) Switches:**
- Eliminates need for separate power supplies for WiFi APs and IP phones
- Simplifies installation and reduces cable clutter
- Centralized power management

**WiFi 6 Access Points:**
- Future-proof technology supporting high device density
- Better performance in crowded environments
- Improved security with WPA3
- Lower latency for real-time applications

**Redundant Equipment:**
- Two core routers, multiple switches provide failover capability
- UPS systems ensure uptime during power outages
- Multiple servers allow load balancing and backup

## 6. Network Management and Monitoring

### 6.1 Network Management Tools
- **Cisco DNA Center:** Centralized management for all Cisco devices
- **SNMP Monitoring:** Real-time monitoring of device health
- **Syslog Server:** Centralized logging for troubleshooting

### 6.2 Security Features
- **Firewall:** Fortinet FortiGate at network edge
- **Network Segmentation:** VLANs separate different traffic types
- **VPN:** Site-to-site encrypted tunnels for branch connections
- **WiFi Security:** WPA3-Enterprise with RADIUS authentication

### 6.3 Quality of Service (QoS)
- **Voice/Video Traffic:** Highest priority for video conferencing
- **Business Applications:** Medium priority for CRM, accounting software
- **General Internet:** Lower priority for web browsing

## References

1. Cisco. (2024). Cisco ISR 4000 Series Integrated Services Routers. https://www.cisco.com/c/en/us/products/routers/4000-series-integrated-services-routers-isr/index.html

2. Cisco. (2024). Cisco Catalyst 9300 Series Switches. https://www.cisco.com/c/en/us/products/switches/catalyst-9300-series-switches/index.html

3. IEEE. (2021). IEEE 802.11ax (WiFi 6) Standard.

4. Fortinet. (2024). FortiGate Next-Generation Firewalls. https://www.fortinet.com/products/next-generation-firewall