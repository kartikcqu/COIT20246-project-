# Network Design
This section gives the detailed network design.

[Assumptions](#assumptions) | [Network Design Diagrams and Justifications](#network-design-diagrams-and-justifications) | [WiFi Design](#wifi-design) | [Address Allocations](#address-allocations) | [Recommended Hardware](#recommended-hardware) | [Plan](./plan.md) | [Cloud Services](./cloud.md) | [Security](./security.md) | [Ethics](./ethics.md) | [Reflection](./reflection.md) | [Return to index](./README.md)

## Assumptions

The list of some of the assumptions that are made for providing the network diagram to the Truelec organization. 
- The **headquarters is located in across the Melbourne area **, which will be primarily used for hosting the central administration, core networking equipment(s), dedicated servers, and security systems.
- Despite the headquarters, the branch offices will be located in the Sydney and Adelaide areas in order to support the regional operational teams.
- For each branch office, it will provide continuous support to approximately **15–30 staff**, whilst the headquarters offers the supports to a larger number of users across multiple departments.
- Some of the centralised services that will be offered will be web, CRM, DNS/DHCP, HR, and accounting are hosted at headquarters, with limited local servers at branch offices.
- Redundancy is required for Internet connectivity, routing, and firewall services to ensure high-end availability.
---

## Network Design Diagrams and Justifications
Truelec is given with the network design that shows a headquarter in Melbourne which is connected to its branches in the Adelaide and Sydney. The given requirements by the Truelec are considered, including all the assumptions made and the design created can be seen underneath. 
![Truelec Network Design – Sydney HQ and Branches](images/Truelec_Network_Design.png)

---

### Design Justification

In the above given network design, the interconnection can be checked between the three sites i.e. Melbourne, Sydney and Adelaide. At the WAN level, the two ISPs are connected in order to achieve high-end redundancy over the network. In case, any ISP faces down time, the secondary ISP will ensure availability is maintained. In the same way, the headquarters also have two routers configured which connects to the two firewalls and two switches. These are also connected in the redundant paths and ensure that if any device faces down time, another device will ensure no link failure related issues are faced. After the redundancy, the scalability is also maintained and to maintain this, the network segmentation is carried out. This ensure the IP addresses are used properly and devices are segmented into different subnets. For example, DMZ network has 42.60.0.0/24 whilst the IoT/CCTV network has 42.40.0.0/24. After the headquarters, in the case of the Sydney and the Adelaide also, the router is connected at both sides and it connects with the branch switch in order to connect WAN with the LAN. This layer two switch further connects with the local server, the wireless access points and other devices connected via the ethernet cables, getting IP from the DHCP pools. 

---

## WiFi Design

In the proposed network design to the Truelec organization, each branch, including the headquarters have enabled with wireless connections. In the headquarter area, the Cisco Aironet Aps are used which offers wireless connectivity to connect IoT devices, laptops, workstations and other devices wirelessly. In the same way, for the branches, the same access point is used and connected to the network to offer wireless coverage and allow the devices to connect wirelessly. The Wi-Fi design created can be seen below for each branch. 

![HQ](images/Wi-Fi_HQ.png)
---

![HQ](images/Wi-Fi_Sydney.png)
---

![HQ](images/Wi-Fi_Adelaide.png)
---

## Address Allocations

| Site | Network / Device | IP Address / Range | Subnet Mask | Purpose |
|------|------------------|--------------------|-------------|---------|
| HQ – Sydney | Primary ISP Gateway | 42.0.0.1 | 255.255.255.0 | Internet access |
| HQ – Sydney | Router 1 (Primary WAN) | 42.0.2.1 | 255.255.255.0 | HQ edge routing |
| HQ – Sydney | Router 2 (Backup WAN) | 42.3.0.1 | 255.255.255.0 | Redundant routing |
| HQ – Sydney | Staff Network | 42.10.0.0 | 255.255.255.0 | Staff workstations |
| HQ – Sydney | Management Network | 42.20.0.0 | 255.255.255.0 | Management PCs |
| HQ – Sydney | WiFi Network | 42.50.0.0 | 255.255.255.0 | Wireless users |
| HQ – Sydney | CCTV / IoT Network | 42.40.0.0 | 255.255.255.0 | Cameras & IoT |
| HQ – Sydney | CCTV NVR | 42.40.0.20 | 255.255.255.0 | Video storage |
| HQ – Sydney | IoT Gateway | 42.40.0.21 | 255.255.255.0 | IoT management |
| HQ – Sydney | DMZ Network | 42.60.0.0 | 255.255.255.0 | Public services |
| HQ – Sydney | Web Server | 42.60.0.10 | 255.255.255.0 | Public web |
| HQ – Sydney | CRM Server | 42.60.0.11 | 255.255.255.0 | CRM application |
| HQ – Sydney | DNS/DHCP Server | 42.60.0.12 | 255.255.255.0 | Name resolution |
| HQ – Sydney | HR/Accounting Server | 42.60.0.13 | 255.255.255.0 | Internal services |
| Brisbane Branch | LAN Network | 74.2.0.0 | 255.255.255.0 | Wired users |
| Brisbane Branch | WiFi Network | 74.2.0.0 | 255.255.255.0 | Wireless users |
| Brisbane Branch | Local Server | 74.2.0.254 | 255.255.255.0 | Branch services |
| Brisbane Branch | CCTV Cameras | 74.2.0.30 | 255.255.255.0 | Surveillance |
| Brisbane Branch | DHCP Pool | 74.2.0.50–74.2.0.200 | 255.255.255.0 | Client devices |
| Brisbane Branch | WAN Link 1 | 74.0.0.0 | 255.255.255.0 | VPN to HQ |
| Brisbane Branch | WAN Link 2 | 74.1.0.0 | 255.255.255.0 | Redundant VPN |
| Adelaide Branch | LAN Network | 74.20.0.0 | 255.255.255.0 | Wired users |
| Adelaide Branch | WiFi Network | 74.20.0.0 | 255.255.255.0 | Wireless users |
| Adelaide Branch | Local Server | 74.20.0.254 | 255.255.255.0 | Branch services |
| Adelaide Branch | CCTV Cameras | 74.20.0.30 | 255.255.255.0 | Surveillance |
| Adelaide Branch | DHCP Pool | 74.20.0.50–74.20.0.200 | 255.255.255.0 | Client devices |
| Adelaide Branch | WAN Link 1 | 74.10.0.0 | 255.255.255.0 | VPN to HQ |
| Adelaide Branch | WAN Link 2 | 74.11.0.0 | 255.255.255.0 | Redundant VPN |

## Recommended Hardware

| Devices | Vendor | Model/Series | Specifications | No. | Cost (AUD) | URL |
|----------|--------------|-------|--------------------|----------|--------------------|-----|
| Edge Router (HQ) | Cisco | ASR 900 Series | Enterprise WAN routing, dual WAN support and high availability | 2 | $6,500 each | https://nexstor.com/wp-content/uploads/2018/05/cisco-asr-900-series-datasheet.pdf |
| Branch Router | Cisco | ASR 900 Series | Secure WAN routing and VPN support | 4 | $4,000 each | https://nexstor.com/wp-content/uploads/2018/05/cisco-asr-900-series-datasheet.pdf |
| Firewall | Fortinet | FAZ-1000F, Fortinet FortiAnalyzer, 192TB Storage/8xGE Ports/RAID Support FAZ-1000F | Stateful firewall, NAT, VPN and HA support | 2 | $35,95 each | https://www.router-switch.com/faz-1000f.html |
| Core Switch | Cisco | Catalyst 3850 | Layer 3 switching, 48 ports and 10G uplinks | 2 | $5,000 each | https://www.cisco.com/c/en/us/support/switches/catalyst-3850-series-switches/series.html |
| DMZ Switch | Cisco | Catalyst 3850 | Layer 3 switching and server aggregation | 1 | $5,000 | https://www.cisco.com/c/en/us/support/switches/catalyst-3850-series-switches/series.html |
| Access Switch | Cisco | WS-C2960L-48TS-LL | 24–48 ports, Gigabit Ethernet and PoE | 6 | $1,200 each | https://www.router-switch.com/ws-c2960l-48ts-ll.html |
| Wireless Access Point | Cisco | Aironet 9120AX | WiFi 6 (802.11ax) and WPA3 security | 4 | $800 each | |
| Server (HQ) | Dell | DELLT640-18, Dell PowerEdge Tower Server, 16C32T | Xeon CPU, ECC RAM and RAID storage | 4 | $4,500 each | https://www.router-switch.com/dell-5u-t640-5218-8g-1-600g-sas-10k-1-h330-dvd-750w-1-3-5-8.html |
| Branch Server | Dell | DELLT640-18, Dell PowerEdge Tower Server, 16C32T | Application hosting and local services | 2 | $3,500 each | https://www.router-switch.com/dell-5u-t640-5218-8g-1-600g-sas-10k-1-h330-dvd-750w-1-3-5-8.html |


