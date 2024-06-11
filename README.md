
# NETWORK DESIGN AND SIMULATION FOR A CRITICAL LARGE COMPANY

**Description:** This project contains the comprehensive network design and simulation report for a critical large company (BB Bank). The report covers network requirements, analysis and design, network map design using Packet Tracer, network system simulation, and network evaluation. It includes detailed descriptions, configurations, and diagrams to illustrate the proposed network infrastructure, ensuring high security, availability, and scalability.

**Author:** Tommy Huynh

**December 2023**

---

## Contents

1. [Network Requirements](#network-requirements)
2. [Network Analysis and Design](#network-analysis-and-design)
   1. [Analysis of Physical Layout](#analysis-of-physical-layout)
      1. [Overview](#overview)
      2. [Layout Survey](#layout-survey)
      3. [Layout Analysis](#layout-analysis)
   2. [Network Design](#network-design)
      1. [Connection Type](#connection-type)
      2. [Network Security](#network-security)
      3. [Surveillance and Peripheral System](#surveillance-and-peripheral-system)
      4. [Virtual Private Network](#virtual-private-network)
         1. [Site-to-Site VPN Configuration](#site-to-site-vpn-configuration)
         2. [Teleworker VPN Configuration](#teleworker-vpn-configuration)
      5. [Virtual Local Area Network](#virtual-local-area-network)
   3. [Network Connection](#network-connection)
      1. [Traffic Overview](#traffic-overview)
      2. [Throughput and Bandwidth](#throughput-and-bandwidth)
      3. [Internet Service Provider Options](#internet-service-provider-options)
      4. [Leased Lines Options](#leased-lines-options)
3. [Design the Network Map Using Packet Tracer](#design-the-network-map-using-packet-tracer)
   1. [Overview](#overview)
   2. [Interconnectivity](#interconnectivity)
      1. [Wide Area Network (WAN) Connectivity](#wide-area-network-wan-connectivity)
      2. [Connectivity Among Departments](#connectivity-among-departments)
      3. [Connectivity Among Devices Within the Same Departments](#connectivity-among-devices-within-the-same-departments)
      4. [Connectivity Among LANs and Internet](#connectivity-among-lans-and-internet)
   3. [VLAN Segmentation](#vlan-segmentation)
   4. [External Networks](#external-networks)
      1. [Demilitarized Zone (DMZ)](#demilitarized-zone-dmz)
      2. [Teleworker Connection](#teleworker-connection)
      3. [Site-to-Site VPN](#site-to-site-vpn)
4. [Network System Simulation](#network-system-simulation)
   1. [Connect Between PCs in the Same VLAN](#connect-between-pcs-in-the-same-vlan)
      1. [Connect Two PCs Inside Operation & Legal Department](#connect-two-pcs-inside-operation-legal-department)
      2. [Connect a PC Connected via Ethernet and a Laptop Connected to Wifi Inside Banking Department](#connect-a-pc-connected-via-ethernet-and-a-laptop-connected-to-wifi-inside-banking-department)
   2. [Connect PCs Between VLANs](#connect-pcs-between-vlans)
      1. [Connect a PC from Operation & Legal to a PC in Banking](#connect-a-pc-from-operation-legal-to-a-pc-in-banking)
      2. [Connect a PC from an HCM Department to a Server](#connect-a-pc-from-an-hcm-department-to-a-server)
   3. [Connect PCs Between Headquarters and Branches](#connect-pcs-between-headquarters-and-branches)
      1. [Connect PC from HCM to a PC in Hanoi](#connect-pc-from-hcm-to-a-pc-in-hanoi)
      2. [Connect PC in Hanoi to Mail Server in HCM](#connect-pc-in-hanoi-to-mail-server-in-hcm)
   4. [Connect to Servers in the DMZ](#connect-to-servers-in-the-dmz)
   5. [No Connections from Customers' Devices to PCs on the LAN](#no-connections-from-customers-devices-to-pcs-on-the-lan)
      1. [Cannot Connect from Customer Laptop to a PC on Floor2](#cannot-connect-from-customer-laptop-to-a-pc-on-floor2)
      2. [Cannot Connect from Customer Laptop to a Server](#cannot-connect-from-customer-laptop-to-a-server)
   6. [Connect to the Internet to a Web Server](#connect-to-the-internet-to-a-web-server)
      1. [Connect from PC HCM Floor2 4 to 8.8.8.8](#connect-from-pc-hcm-floor2-4-to-8888)
      2. [Connect from PC 1 (Hanoi) to Web Server Using Web Browser via HTTP](#connect-from-pc-1-hanoi-to-web-server-using-web-browser-via-http)
5. [Network Evaluation](#network-evaluation)
   1. [Security Assessment](#security-assessment)
   2. [Scalability Assessment](#scalability-assessment)
   3. [Unresolved Issues](#unresolved-issues)
   4. [Future Design Directions](#future-design-directions)

## Network Requirements

BB Bank, a company that asked us to design a computer network for, laid out their requirements:

- The Headquarter:
  - Located in Ho Chi Minh City.
  - Has 120 workstations, 5 servers, and 12 or more networking devices.
- The Branches:
  - 1 located in Da Nang, another in Ha Noi.
  - Has 30 workstations, 3 servers, and 5 or more networking devices for each branch.
- Usage of new technologies for network infrastructure.
- High security, high availability, robustness when problems occur, ease of upgrading the system.
- A VPN configuration for site-to-site and for a teleworker to connect to Company LAN.
- A surveillance camera system for the Company.
- Connection between Headquarter and Branches by 2 leased lines for WAN connection.
- All traffic to the Internet passes through the Headquarters subnet, with 2 xDSL for Internet access with a load-balancing mechanism.
- The dataflows and workload of the network can be summarized as:
  - Servers for software updates, web access, and database access,... The total download estimate is about 1000 MB/day and the upload estimate is 2000 MB/day for each server.
  - Each workstation is used for Web browsing, document downloads, and customer transactions,... The total download estimate is about 500 MB/day and the upload estimate is 100 MB/day.
  - WiFi-connected devices from customers’ access for downloading are about 500 MB/day.
  - The system peak at 9 AM-11 AM and 3 PM-4 PM, with 80% of dataflows belonging to these timeframes.
- Is estimated to have a growth rate of 20% in 5 years (in terms of the number of users, network load, branch extensions,...).

## Network Analysis and Design

### Analysis of Physical Layout

#### Overview

The network design should meet the network requirements, with many options suggested along with advantages, disadvantages, and cost. Therefore, we divide the system into smaller parts and focus on analyzing each part.

We begin with a survey and design a network layout for the company, then give options for network schematic. Second is the analysis for each equipment and each schematic in general. Thirdly, we calculate throughput and recommend appropriate plans from ISP (Internet Service Provider). Finally, we will design and simulate a specific network layout from the recommended list.

#### Layout Survey

A survey on the office’s locations should record the following details:

- Physical layout of the buildings:
  - Area for installation of network devices, security devices, and peripheral devices.
  - Physical obstacles and interference (building’s electricity, environment’s magnetism,...) that may have adverse effects on network signal traversal.
- Department-specific and room-specific:
  - Expected number of people a room may have.
  - Functionality and security constraints of each room.

#### Layout Analysis

Assuming that a study upon the BB Bank offices has completed, we got the departments of the Headquarter, 2 Branches, and the physical layout of the 3 offices as follows.

A normal work room will have the following installation layout:

| Branch      | Department Name       | Number of Workstations |
|-------------|-----------------------|------------------------|
| Headquarter | Banking               | 20                     |
| Headquarter | Operations & Legal    | 20                     |
| Headquarter | Risk Management       | 20                     |
| Headquarter | Finance               | 20                     |
| Headquarter | Human Resources       | 20                     |
| Headquarter | IT                    | 10                     |
| Headquarter | Administration        | 10                     |
| Branches    | Banking               | 10                     |
| Branches    | Operations & Legal    | 10                     |
| Branches    | IT                    | 5                      |
| Branches    | Administration        | 5                      |

**Figure 1: Headquarter Building Layout**

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/4758c142-8780-48d6-9422-6a8e4931ed95)


**Figure 2: Branch Building Layout**

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/fc2c9024-b758-42c7-b716-979a2ff4589e)


**Figure 3: Installation Layout for a Room**

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/e55fb49f-e317-4c1b-9b82-4292f67feb8c)


### Network Design

#### Connection Type

We consider the first pair of options to choose from, which is the connection type of workstations. Firstly, a router (Cisco ISR4331/K9) must be bought for HQ and each branch, along with 4 Ethernet switch (Cisco 4-Port Gigabit Ethernet Switch NIM NIM-ES2-4).

Furthermore, a company using a wired network must also have Wi-Fi access points to accommodate customers and peripheral devices connection.

With wired connection, the newest and most stable technology today is Ethernet-Cat8. Its advantage is that it can offer up to 40Gbps speed and reduce interference, while its principal disadvantage is the cable is less flexible. We still need 11 switches (Cisco 24 Port Catalyst 2960 WS-C2960-24TC-L) and 11 lightweight Wi-Fi access points (TPLink Archer C54) for 7 floors of HQ and 2 floors of each branch.

With wireless connection, we can choose 11 access points of Wi-Fi 6E technology (Cisco CW9162I-MR 802.11ax Wi-Fi 6E 2x2:2 Access Point). This option's advantage is it's not limited by the number of Ethernet ports while its disadvantage lies in interference from many workstations trying to access the Internet.

Each data with their typical specifications and costs are as follows:

**Router: Cisco ISR4331/K9**

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/dfeff9a9-e08e-42b3-94c1-64ac07cd67c9)


- Cost: 25,000,000 VND
- Aggregate Throughput: 100 Mbps to 300 Mbps
- Total onboard WAN or LAN 10/100/1000 ports: 3
- RJ45-based ports: 2
- SFP-based ports: 2
- Enhanced service-module (SM-X) slot: 1
- NIM (Network Interface Modules) slots: 2
- Onboard ISC slot: 1
- Memory: 4 GB (default) / 16 GB (maximum)
- Flash Memory: 4 GB (default) / 16 GB (maximum)
- Power-supply options: Internal: AC and PoE
- Rack height: 1 RU
- Dimensions (H x W x D): 44.45 x 438.15 x 438.15 mm
- Package Weight: 12.96 Kg

**Network Interface Card: Cisco 4-Port Gigabit Ethernet Switch NIM NIM-ES2-4**

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/28b9982b-7407-4dc9-abb9-c54874e92967)

- Cost: 10,000,000 VND
- Form factor: Single-wide NIM
- Dimensions: 0.8 x 3.1 x 4.8 in.
- Weight: 79g (0.17 lb)
- Standards: IEEE 802.3, 802.1q, 802.1X, RFC 2284, RFC 1213, and more
- Manageability:
  - SNMP and Telnet support
  - Embedded RMON agent
  - SPAN port for monitoring
  - TFTP for software upgrades
  - LEDs for status indication
- Connectivity:
  - Ports: 10BASE-T, 100BASE-TX, 1000BASE-TX
  - Cabling: RJ-45 connectors, UTP cables
- Power Requirements:
  - Internal power supply with optional PoE
  - DC power support on selected models
- Software Support:
  - Cisco IOS-XE Software Release 3.15
- Environmental:
  - Operating temperature: 32° to 104°F
  - Operating humidity: 10 to 90 percent
  - Altitude: Up to 15,000 ft
- Regulatory Compliance: Meets Cisco 4000 Series router standards

**Switch: Cisco 24 Port Catalyst 2960 WS-C2960-24TC-L**

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/150ec438-3119-481a-affa-b466a87db229)


- Cost: 15,000,000 VND
- Rack Mount Standard: Rack-mountable 1U
- Feature Set: LAN Base
- Uplink Interfaces: 2 (SFP or 1000BASE-T)
- Ports: 24 x 10/100 Ethernet Ports
- Forwarding Bandwidth: 16 Gbps
- Forwarding Rate: 6.5 Mpps
- RAM: 128 MB
- Flash Memory: 64 MB
- Dimensions: 4.4cm x 45.0 cm x 24.2 cm
- Weight: 7.73 Kg

**Baseus Cat8 40-Gigabit RJ45 Network Cable**

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/cb6c0d3c-04b3-40e4-b4b5-4d5d67162771)


- Cost: 400,000 VND/cable of 10 meters
- Transmission speed: 40 Gbps
- Bandwidth: 2000 MHz
- Shielding: 4 layers
- 30 AWG pure copper wire core
- 48-strand braided cable jacket

**Access Point: TPLink Archer C54**

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/0bd0bd3d-844a-46c9-ae34-d90e4eaf87df)


- Cost: 400,000 VND
- WiFi
  - Standard: Wi-Fi 5
  - Speed: 867 Mbps (5 GHz), 300 Mbps (2.4 GHz)
  - Coverage: 3-bedroom apartment, 4× antennas
  - Capacity: Moderate
  - Dual Band: Yes
  - MU-MIMO: 2×2
- Hardware
  - Ethernet Ports: 1× WAN, 4× LAN (10/100 Mbps)
- Security
  - Wi-Fi Encryption: WPA, WPA2
- Software
  - Network Security: SPI Firewall, Access Control
  - Guest Network: 1× 5 GHz, 1× 2.4 GHz

**Access Point: Cisco CW9162I-MR 802.11ax Wi-Fi 6E 2x2:2 Access Point**

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/a2709898-7432-4fc0-ab4e-c321b70227fa)


- Cost: 25,000,000 VND
- Part Numbers: CW9162I-MR
- Software: 802.11ax
  - MU-MIMO: 2x2 (6 GHz up/down, 2.4 GHz and 5 GHz down)
  - Features: OFDMA, TWT, BSS coloring, MRC, 802.11ax beamforming
  - Channels: 20/40/80/160 MHz (6 GHz), 20/40/80 MHz (5 GHz), 20 MHz (2.4 GHz)
  - PHY Data Rates: Up to 3.9 Gbps, Packet Aggregation: A-MPDU, A-MSDU
  - DFS, CSD, WPA3 support
- Integrated Antenna:
  - 2.4 GHz: 4 dBi, internal omnidirectional
  - 5 GHz: 5 dBi, internal omnidirectional
  - 6 GHz: 5 dBi, internal omnidirectional
- Interfaces:
  - 1x 100M/1000M/2.5G Multigigabit Ethernet, RJ-45
  - Management console port, RJ-45, USB 2.0 (4.5W)
- Indicators:
  - Status LED: boot loader, association, operating status, warnings, errors
- Dimensions: 7.8 x 7.8 x 1.7 in. (200 x 200 x 44.45 mm)
- Weight: 2.05 lb. (0.93 kg)
- System Memory: 2048 MB DRAM, 1024 MB flash

#### Network Security

A security solution can be recommended following the DMZ architecture. A DMZ will contain a Firewall and servers that handle client or outgoing interactions.

**Firewall: Cisco ASA5506-SEC-BUN-K9**

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/7fcbd8b1-1c68-41f3-84ad-ca495d6d68c9)


- Cost: 25,000,000 VND
- Throughput: Application Control (AVC) - 250 Mbps
- Throughput: Application Control (AVC) and IPS - 125 Mbps
- Max Concurrent Sessions: 20,000 (50,000 with License)
- Max New Connections per Second: 5,000
- Supported Applications: 3,000+
- URL Categories: 80+
- Categorized URLs: 280 million+
- Stateful Inspection Throughput (Max): 750 Mbps
- Stateful Inspection Throughput (Multiprotocol): 300 Mbps
- 3DES/AES VPN Throughput: 100 Mbps
- Users/Nodes: Unlimited

**Software: Cisco SEC-K9 License**

- Cost: 27,258,507 VND
- Purpose: Enhances security on Cisco routers and switches.
- Key Features:
  - VPN support for secure remote connections.
  - Advanced encryption for data security.
  - Integrated firewall capabilities.
  - Intrusion Prevention System (IPS) for network protection.
  - Content filtering options.

#### Surveillance and Peripheral System

Another choice for BB Bank is whether the surveillance and peripheral system is designed upon an Internet of Things (IoT) framework or each independent device handles different functions.

Consider the latter option, we can design a system where the surveillance system transmits its data to the IT department over the nearest WiFi access point or router, with peripheral devices like fire monitors, and sirens for money storage, each function independently. The upsides of this system are its independence between devices, not having a single point of failure, cheaper than the other option while its downsides are BB Bank having less ability to control it.

An IoT system can be designed with consideration of BB Bank’s 3 locations' physical layout, connected directly into the IT department VLAN. The system’s function is to control peripheral devices and the surveillance system, itself being controlled by the IT department. Such a system helps BB Bank to have greater control over workspace and can improve the performance of the whole system while its downside is more expensive than the previous option, requires expertise in the IT department to maintain the system and have a single point of failure.

Considering just the surveillance system, a proposal upon the system can be made as follows:

**Camera: DS-2GN5750-HH**

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/5431d1bb-a704-4825-a17a-16f37dd743d8)

- Cost: 4.335,000 VND
- High-quality imaging with 4 MP resolution
- Excellent low-light performance
- Efficient H.265+ compression technology
- Water and dust resistant (IP67)
- 24/7 colorful imaging
- Support Human and Vehicle Detection

| Floor | Cameras |
|-------|---------|
| 1     | 3       |
| 2-7   | 2       |

**Table 2: Camera on each floor at Headquarter**

| Floor | Cameras |
|-------|---------|
| 1     | 3       |
| 2     | 5       |

**Table 3: Camera on each floor at Branches**

#### Virtual Private Network

A VPN configuration for BB Bank can be assigned upon each department. A proposal for VPN configuration is as follows:

##### Site-to-Site VPN Configuration

Below are our requirements for Site-to-Site VPN setup:

- For interconnecting the bank’s main office with its regional branches, a site-to-site VPN will be established. This will use IPSec protocol to ensure secure and encrypted communication between sites.
- Each branch will have a dedicated VPN gateway that will connect to the main office’s central VPN server. This setup will allow seamless sharing of resources and maintain a consistent security posture.
- The VPN will be configured to support dynamic routing protocols like OSPF or BGP to ensure efficient network traffic management.

With that, the solution we choose is Cisco Meraki MX Series:

- Features: Offers integrated SD-WAN and security features. It’s cloud-managed, simplifying complex VPN setups.
- Costs: From 14,500,000 VND for the cheapest model (MX67)

##### Teleworker VPN Configuration

Below are our requirements for Teleworker VPN setup:

- Remote employees or teleworkers will be provided with VPN client software that can be installed on their work devices. This client will facilitate a secure connection to the BB Bank’s LAN.
- The teleworker VPN will use SSL/TLS for encryption, offering a balance of strong security and ease of use without the need for additional hardware.
- Multi-factor authentication (MFA) will be implemented to enhance security. This ensures that only authorized personnel can access the bank’s network remotely.

With that, the solution we choose is Cisco AnyConnect Secure Mobility Client:

- Features: Offers unified endpoint compliance, robust network access security, web and roaming protection, network visibility, support for mobile devices, and advanced VPN options for secure and flexible remote connectivity.
- Costs: 100,943,200 VND for the 100 Simultaneous (eDelivery) license for 100 connections.

#### Virtual Local Area Network

VLANs will be implemented across BB Bank’s network to segment the network into smaller, manageable parts. This segmentation helps in improving performance, enhancing security, and simplifying network management. VLANs effectively segregate traffic from different departments, ensuring operational efficiency and data privacy.

Each department within BB Bank (e.g., Accounting, Human Resources, Customer Service) will have its own VLAN. This approach ensures that the traffic and resources relevant to each department are isolated, thereby reducing unnecessary traffic and enhancing security.

The size of each VLAN should be based upon the number of personnel, which we can only approximate the upper limit, and the functionality of each department.

| VLAN Name         | VLAN Size | Subnet             |
|-------------------|-----------|--------------------|
| Floor 1           | 256       | 192.168.10.1/24    |
| Operations & Legal| 256       | 192.168.20.1/24    |
| Banking           | 256       | 192.168.30.1/24    |
| Risk Management   | 256       | 192.168.40.1/24    |
| Human Resources   | 256       | 192.168.50.1/24    |
| Finance           | 256       | 192.168.60.1/24    |
| IT                | 256       | 192.168.60.1/24    |
| Administration    | 256       | 192.168.70.1/24    |

**Table 4: VPN IP Plan Table**

Except for Floor 1, which contains a mix of IT computers, Servers, and Customer devices, each floor hosts a different department and is segmented with a separate VLAN.

### Network Connection

In terms of network connectivity, we need to calculate the required throughput and expected bandwidth to ensure seamless data transfer and optimal performance for the interconnected devices and systems.

- Bandwidth: refers to the maximum rate of data transfer through a network, typically measured in Megabits per second (Mbps), indicating the capacity for information flow.
- Throughput is the actual amount of data transmitted successfully over a communication channel in a given period, reflecting the practical efficiency of data transfer.

#### Traffic Overview

The dataflow and workload of the system at the headquarter can be categorized as follows:

- Servers:
  Total upload and download of 5 servers:
  - Download: 1000× 5 = 5000 MB/day.
  - Upload: 2000× 5 = 10000 MB/day.
- Workstations:
  Total upload and download of 120 workstations:
  - Download: 500× 120 = 60000 MB/day.
  - Upload: 100× 120 = 12000 MB/day.
- Customers’ devices:
  With an estimated 50 clients per day, we have:
  - Download: 500× 50 = 25000 MB/day.
  - Upload: 0 MB/day.

In summary, DHQ = 90000 MB/day and UHQ = 22000 MB/day.

On the other hand, The dataflow and workload of the system at each branch can be categorized as follows:

- Servers:
  Total upload and download of 3 servers:
  - Download: 1000× 3 = 3000 MB/day.
  - Upload: 2000× 3 = 6000 MB/day.
- Workstations:
  Total upload and download of 30 workstations:
  - Download: 500× 30 = 15000 MB/day.
  - Upload: 100× 30 = 3000 MB/day.
- Customers’ devices:
  With an estimated 30 clients per day, we have:
  - Download: 500× 50 = 15000 MB/day.
  - Upload: 0 MB/day.

In summary, DB = 33000 MB/day and UB = 9000 MB/day.

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/f3df33f5-d54e-47fe-b11a-61c095baee5d)


**Figure 12: Overview of BB Bank’s Network Dataflow at the present**

#### Throughput and Bandwidth

With 80% of the dataflow being concentrated in peak hours of 9 AM-11 AM and 3 PM-4 PM, we can calculate average throughput in these 3 peak hours. We also need to accommodate a further 20% for future growth for both device usage and the number of devices on the Bank’s network:

- Download: \( \frac{156000 \times 0.8 \times 1.22 \times 8}{3 \times 60 \times 60} = 133.12 \) Mbps.
- Upload: \( \frac{40000 \times 0.8 \times 1.22 \times 8}{3 \times 60 \times 60} = 34.1333 \) Mbps.

As dataflow from peak hours establishes the rate for the average throughput, ISPs are expected to provide a bandwidth of more than 134 Mbps in download and 35 Mbps in upload to guarantee business functionality.

#### Internet Service Provider Options

Some options for Internet Service Provider (ISP) can be listed.

**VNPT: FIBERVIP6**

This is particularly useful owing to its bandwidth meeting the required bandwidth, which is calculated above. Static WAN helps BB Bank with an identifiable, unchanged IP address, particularly useful with BB Bank’s DNS server.

- Cost: 1,000,000 VND/month, installation cost not included
- 1 Static IPv4 WAN
- 1 Subnet/56 IPv6 Static LAN
- Domestic Speed: 200 Mbps

**FPT: SUPER250**

Another viable option for BB Bank. While it does not have 1 Subnet/56 IPv6 Static LAN, it does have a high international speed with cost more or less the same.

- Cost: 1,045,000 VND/month, 100,000 VND for installation cost
- 1 Static IPv4 WAN
- Domestic Speed: 250 Mbps
- International Speed: up to 10.8 Mbps

**Viettel: F200N**

Another good option. However, the international speed of Viettel’s is less than FPT’s.

- Cost: 1,100,000 VND/month, installation cost not included
- 1 Static IPv4 WAN
- Domestic Speed: 200 Mbps
- International Speed: 2 Mbps

#### Leased Lines Options

Some options for Leased Lines can be listed.

**VNPT**

Very high monthly cost, VNPT provides a bandwidth of 34 Mbps, suitable for Branch connection to Headquarter.

- Cost: 51,120,000 VND/month, 30,000,000 VND installation cost, each line
- Bandwidth: 34 Mbps

**Viettel**

Higher installation cost but have lower monthly cost, this option is obviously much better for BB Bank.

- Cost: 41,498,000 VND/month, 40,000,000 VND installation cost, each line
- Bandwidth: 34 Mbps

### Design the Network Map Using Packet Tracer

#### Overview

Included below is the full view of the Packet Tracer implementation.

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/e28c3887-35ad-49d1-82b6-df6467bdeed5)


**Figure 13: Overview of BBBank network design in Packet Tracer**

The network view features several components of the network system:

- Headquarter branch: Contains seven floors that host different departments, each with several workstations, the Router gateway that sits between all branches, as well as several servers and intermediate devices.
- Da Nang branch and Ha Noi branches: Each features a smaller set of devices compared to the headquarter branch such as workstations and their local servers.
- External area: The design also features some areas from the network outside of the branches. They are the DMZ area, the ”Internet”, and the connection from Teleworker.

#### Interconnectivity

##### Wide Area Network (WAN) Connectivity

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/5da5b10f-ea66-44e2-a137-5d5824539d4b)


**Figure 14: OSPF 1 Area 0 WAN**

The diagram above depicts the Wide Area Network (WAN) connectivity for BB Bank with three branches, utilizing OSPF (Open Shortest Path First) as the routing protocol with Area 0 configuration. OSPF is a routing protocol used within larger networks to distribute IP routing information using link-state algorithm.

- OSPF Area 0 (Backbone Area):
  - Routers within this section are part of Area 0, the backbone area of the OSPF networked environments.
  - The other sites (eg. branches and externals) in the network must connect to Area 0, making it central to OSPF route propagation and ensuring all areas can communicate effectively.
- The Router-PT HCM Gateway:
  - Acts as a gateway for Headquarter and is the core router connecting all branch routers.
  - Acts as the point of the connection to other networks, such as the Internet, DMZ area. In the other words, Da Nang and Ha Noi branches are to access the rest of the external network or the internet (depicted on the left of this diagram) through this link.
  - The gateway connects to the primary routers of each branch using dedicated leased lines to ensure critical connections and loads.
- Router-PT HQ/HANOI/DANANG:
  - The primary routers for each branch that bridge the network between the internal and external sites.
  - Each connects to the internal network of the branch using Copper Straight-Through.

##### Connectivity Among Departments

Sits in between the primary routers and the internal network end devices are three Core Switch in all branches:

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/87078d96-0fc4-4c44-b8dc-cd7055f7a63b)


**Figure 15: Hanoi Site Design**

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/aa82ad56-9ec6-4b7a-9cb8-0722e5ef8b9a)



**Figure 16: Danang Site Design**

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/fabdfe96-5d8d-4f3d-b5e7-962e109cc26c)

**Figure 17: Ho Chi Minh Core Switch**

In this architecture, the core switch acts as a central for each branch’s network. It is responsible for routing and switching traffic efficiently to ensure seamless connectivity across the company’s various departments and services.

Each floor or department within the branches has its own access switch, which connects back to this central core switch, forming a star topology that centralizes network traffic management.

The VLANs span multiple switches using trunk links. Trunk links carry traffic from all VLANs by default between the switches, allowing devices on different VLANs (in this case, workstations on different floors/different departments) to communicate through the Layer 3 device.

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/8eceef73-c43c-4d20-8501-e97efdd589c8)


**Figure 18: End Devices using DHCP to obtain IPs**

A configuration is in place to allow each device to obtain an IP Address through DHCP. For example, the device below on the second floor (which is in VLAN 20) obtains the expected IP address within its submask affordance.

Some other devices like IP Camera and Server are assigned a fixed IP address for consistent access.

##### Connectivity Among Devices Within the Same Departments

End devices on each floors/departments are connected to a floor-level switch. Allowing each of them to connect with each other.

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/c9a742e5-df77-46a4-bc5a-54ae6954a912)


**Figure 19: Floor-level switches**

##### Connectivity Among LANs and Internet

As you can see, local IP addresses have been translated into public IP addresses. For example, in the picture, the IP address of the PC2 on the second floor of Danang branch, which is translated from 172.16.20.11 into 209.165.0.2 (global IP address in the outside interface Serial0/1/1 of the Main Gateway).

#### VLAN Segmentation

The following section will focus on explaining the setup in HCM Branch as it is the most complex, while those in the Hanoi and Danang branches are similar but on a smaller scale.

The network is logically divided into several VLANs, separating critical servers, user groups, and guest traffic. This segmentation enhances security and traffic management, with inter-VLAN routing handled by layer 3 switches (The ”core switches” mentioned in the section above) to optimize traffic flow.

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/3ba388ba-1497-4dac-916b-958edf40b74b)


**Figure 20: NAT**

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/a77c4956-97dd-4e21-a62b-f62e69f31c8b)


**Figure 21: Core Switch VLAN Database**

The core switch is set up to include different VLAN Configuration, as shown in the design in section 2.2.5.

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/22f5a214-496d-4f0e-a274-c29a127a15d4)


**Figure 22: Core Switch Interfaces**

Different switches from each department are connected to different ports on the core switches and they are configured to be assigned different VLANs as shown in the dialog above.

#### External Networks

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/ff00a51a-3c30-45ce-bf37-3f75c2576c79)


**Figure 23: External Network Components**

The diagram above presents a multi-faceted network with components for internet access, a DMZ for publicly accessible services, and remote site connectivity for a teleworker, all of which are interfaced via the Main Gateway router connected to the WAN area as explained above in section 3.1.2.a.

##### Demilitarized Zone (DMZ)

In computer networks, a DMZ, or demilitarized zone, is a physical or logical subnet that separates a local area network (LAN) from other untrusted networks – usually, the public internet. DMZs are also known as perimeter networks or screened subnetworks.

Servers and resources in the DMZ are accessible from the internet, but the rest of the internal LAN remains unreachable. This approach provides an additional layer of security to the LAN as it restricts a hacker’s ability to directly access internal servers and data from the internet.

DMZ networks are often used for the following:

- Isolate and keep potential target systems separate from internal networks;
- Reduce and control access to those systems by external users; and
- Host corporate resources to make some of them available to authorized external users.

##### Teleworker Connection

With a VPN, the institution’s inter-office traffic is sent over the public Internet rather than over a physically independent network. But to provide confidentiality, the inter-office traffic is encrypted before it enters the public Internet.

Here the institution consists of a headquarters, 2 branch offices, and a teleworker that typically accesses the Internet from their home. In this VPN, whenever two hosts within headquarters send IP datagrams to each other or whenever two hosts within the branch office want to communicate, they use good-old vanilla IPv4 (that is, without IPsec services). However, when two of the institution’s hosts communicate over a path that traverses the public Internet, the traffic is encrypted before it enters the Internet.

The VPN configuration is:

- Group Name: cisco
- Group Key: Cisco@123
- Host IP (Server IP): 169.113.0.1
- Username: admin
- Password: Admin@123

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/9d1703a4-7d5c-4507-96e3-b6eb9e59100e)


**Figure 24: Teleworker trying to access VPN**

The teleworker has accessed the VPN successfully:

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/3fe9fdb0-25ab-4eb2-a632-00edcc9f24a1)


**Figure 25: Teleworker accessing VPN successfully**

Now the teleworker can access the web server in the Headquarters.

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/eda249e9-e6b7-4476-aafb-7e7a02b1f526)


**Figure 26: Teleworker can ping the web server in HQ**

##### Site-to-Site VPN

After connection between 1 PC in Hanoi and 1 PC in Danang has been established, the VPN tunnel is set to Active mode, so the site-to-site VPN information is displayed in both routers.

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/b3d26ec7-994a-4afd-b306-6ec8898f86d4)


**Figure 27: Teleworker can ping the web server in HQ**

### Network System Simulation

Several tests are performed to confirm the connectivity as in the requirements. Note that the IPs from PCs of some of the tests below may change from test-to-test due to DHCP.

We are going to use PING test to check for connectivity and TRACERT command to confirm the routes in some tests like Internet connectivity.

#### Connect Between PCs in the Same VLAN

##### Connect Two PCs Inside Operation & Legal Department

A ping test is performed between PC HCM Floor2 4 (192.168.20.15) and PC HCM Floor2 5 (192.168.20.16).

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/6d30d6c8-e27b-48e3-a5d7-e647a5e06da3)


**Figure 28: PC HCM Floor2 4 and PC HCM Floor2 5**

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/97e84f01-0d01-42ea-b6f4-d997cdac5054) ![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/3855cbd7-b659-4add-b270-d261065577af)



**Figure 29: Ping results between PC HCM Floor2 4 and PC HCM Floor2 5**

##### Connect a PC Connected via Ethernet and a Laptop Connected to Wifi Inside Banking Department

A ping test is performed between PC HCM Floor3 4 (192.168.30.12) and Laptop HCM Floor3 1 (192.168.30.11).

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/3cf0c049-0eae-4dc3-b4f7-cf19089adb44)


**Figure 30: PC HCM Floor3 4 and Laptop HCM Floor3 1**

![Ping results between PC HCM Floor3 4 and Laptop HCM Floor3 1](./images/ping_results_floor3_4_and_laptop.png)

**Figure 31: Ping results between PC HCM Floor3 4 and Laptop HCM Floor3 1**

#### Connect PCs Between VLANs

##### Connect a PC from Operation & Legal to a PC in Banking

A ping test is performed between PC HCM Floor2 4 (192.168.20.15) and PC HCM Floor3 4 (192.168.30.12).

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/f3d7c4cb-c1f9-49c5-9b2b-11c3f003b3db)



**Figure 32: PC HCM Floor2 4 and PC HCM Floor3 4**

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/2c4dd975-9b94-4adf-858f-fdfa435e67ec)


**Figure 33: Ping results between PC HCM Floor2 4 and PC HCM Floor3 4**

##### Connect a PC from an HCM Department to a Server

A ping test is performed between PC HCM Floor2 4 (192.168.20.15) and Server Mail (192.168.10.30).

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/23aa2cf2-cd32-4732-a016-40e39f4ac7b0)


**Figure 34: PC HCM Floor2 4 and Server Mail**

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/524795bc-bb5e-40db-bbd5-113d148ac86e)


**Figure 35: Ping result for PC HCM Floor2 4 to Server Mail**

#### Connect PCs Between Headquarters and Branches

##### Connect PC from HCM to a PC in Hanoi

To verify the connection of PCs between Headquarter and branches, we ping a PC in HANOI branch (172.16.20.11) from a PC in HCM (192.168.20.11).

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/f05f58be-3bbc-482b-bc9b-9470301a3039)


**Figure 36: PC HCM Floor2 4 and PC1 (HANOI)**

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/38b6a0d9-b67d-49fc-b2f4-6f1d1702cdd2)

**Figure 37: Ping result between PC HCM Floor2 4 and PC1 (HANOI)**

##### Connect PC in Hanoi to Mail Server in HCM

We also test the connection from a PC in Hanoi (172.16.20.11) to access a mail server (192.168.10.10) in HCM.

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/3ee37023-22ad-4d02-a1eb-5a5505fb0516)


**Figure 38: Hanoi PC and HCM Mail Server**

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/b452fc88-200b-4543-86fe-15169ffe4559)


**Figure 39: Ping result for a PC in Hanoi to Mail Server in HCM**

#### Connect to Servers in the DMZ

A ping test is performed between PC in HCM branch and a server in the DMZ.

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/baf787f9-ac23-4ab1-bb82-bc0926089e98)

**Figure 40: PC HCM Floor2 4 and DMZ Server**

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/c921dbbe-c63e-4cae-b637-4ceddef71bcd)


**Figure 41: Ping result from PC HCM Floor2 4 to DMZ Server**

#### No Connections from Customers' Devices to PCs on the LAN

Laptops from customers connected to the Customer WIFI are blocked from accessing the rest of the network using ACL/Firewall.

##### Cannot Connect from Customer Laptop to a PC on Floor2

A ping test is performed between Laptop0 by customer (169.254.42.232) to PC HCM Floor2 4 (192.168.20.13) to confirm there is no connection.

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/76390e51-4e5f-4ec2-b92b-f74ae036d429)


**Figure 42: Failed Ping result from Laptop Guest (customer’s) to PC HCM Floor2 4**

##### Cannot Connect from Customer Laptop to a Server

A ping test is performed between Laptop0 by customer (192.168.10.12) to Server Mail (192.168.10.30) to confirm there is no connection.

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/b37551bd-b2b7-4178-8891-44da482360f1)


**Figure 43: Failed ping request from Laptop Guest (customer’s) and Server Data**

#### Connect to the Internet to a Web Server

##### Connect from PC HCM Floor2 4 to 8.8.8.8

A ping test and trace route is performed from a PC in HCM to server 8.8.8.8 on the internet to confirm the connection and routing to the internet.

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/be547c6e-e908-4687-9574-fdd04a33dd51)


**Figure 44: PC HCM Floor2 4 and internet Web Server**

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/b5e325b0-cc06-4ece-b85f-419ef04dbbf0)


**Figure 45: Ping and trace route from a PC in HCM to the Internet**

##### Connect from PC 1 (Hanoi) to Web Server Using Web Browser via HTTP

Alternatively, we also attempt to use the web browser to access the 8.8.8.8 server on the internet.

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/5cb58483-928c-4b87-8354-e45c8087538c)


**Figure 46: PC in Hanoi to 8.8.8.8 server**

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/1ff2df76-276b-4f1c-b030-a18e5a650dd6)


**Figure 47: Access 8.8.8.8 from a PC in Hanoi**

#### Security

In this part, we added a security license called K9 for the router

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/a087b4c2-dbd1-4652-bcb9-324ec930991f)

**Figure 48: Router equipped with Security K9 license**

##### Firewall

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/9338a9d6-27e1-4a5e-858c-3218f89e92b1)


**Figure 49: Firewall**

The internal LAN consists of Headquarters and 2 branches which sends traffic to the DMZ and Internet. The DMZ can send and receive traffic from LAN and Internet. The Internet cannot send the traffic to the internal LAN. It is blocked by the firewall and the Intrusion Prevention System (IPS) in the Main Gateway router.

![image](https://github.com/tnpfighter/Internetworking_Project/assets/106922908/fadc70da-1684-4331-b0c5-f320c7a25509)


**Figure 50: Intrusion Prevention System**

The traffic from ISP server is prevented by the Main Gateway router when it attempts to send ICMP packets to the Mail server in the Headquarters due to firewalls and IPS, which send SYSLOG to the Sys Log server in the IT room.

### Network Evaluation

#### Security Assessment

A company’s system must be robust and secure to protect important information, business strategies, and partner contracts. Therefore, the system must meet certain minimum security requirements such as:

- User access control.
- Early prevention of unauthorized access.
- Immediate alerts when there are unauthorized attempts.

This has been implemented and demonstrated in the section above.

#### Scalability Assessment

- The system should be designed for easy expansion (adding devices, network cables, etc.) to accommodate the growth needs of the bank, both at the headquarters and its branches.
- Currently, the main headquarters has about 120 workstations spread over 7 floors, each floor having departments with 10-30 workstations. As per the current design, each floor uses 2 24-port switches (excluding one port connected to the main switch), which allows 47 ports, allowing for more devices to be connected as staff numbers increase.

#### Unresolved Issues

- The system still has many centralized connection points (core switches, core routers), causing system-wide disruptions when these devices fail.
- The design could not be confirmed to meet daily download and upload requirements.
- Being primarily theory-based, the design may not fully align with practical realities.
- The cost of Cisco network devices is high, though reductions are possible in some areas.

#### Future Design Directions

- Find alternatives to Cisco devices to save cost.
- Design to ensure the network is unclogged, meeting daily system download and upload capacity requirements.
- Thoroughly assess practical needs, equipment costs, and design expenses to create a network that meets both system requirements and cost considerations.
- Implement fail-safe so that a failure in one important node (such as a core switch) does not bring down the whole system.


