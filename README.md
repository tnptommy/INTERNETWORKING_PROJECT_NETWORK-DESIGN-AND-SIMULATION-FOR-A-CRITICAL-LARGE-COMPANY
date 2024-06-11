# Network Design and Simulation for a Critical Large Company


---

## Table of Contents

1. [Network Requirements](#1-network-requirements)
2. [Network Analysis and Design](#2-network-analysis-and-design)
   - [Analysis of Physical Layout](#21-analysis-of-physical-layout)
     - [Overview](#211-overview)
     - [Layout Survey](#212-layout-survey)
     - [Layout Analysis](#213-layout-analysis)
   - [Network Design](#22-network-design)
     - [Connection Type](#221-connection-type)
     - [Network Security](#222-network-security)
     - [Surveillance and Peripheral System](#223-surveillance-and-peripheral-system)
     - [Virtual Private Network](#224-virtual-private-network)
       - [Site-to-Site VPN Configuration](#224a-site-to-site-vpn-configuration)
       - [Teleworker VPN Configuration](#224b-teleworker-vpn-configuration)
     - [Virtual Local Area Network](#225-virtual-local-area-network)
   - [Network Connection](#23-network-connection)
     - [Traffic Overview](#231-traffic-overview)
     - [Throughput and Bandwidth](#232-throughput-and-bandwidth)
     - [Internet Service Provider Options](#233-internet-service-provider-options)
     - [Leased Lines Options](#234-leased-lines-options)
3. [Design the Network Map using Packet Tracer](#3-design-the-network-map-using-packet-tracer)
   - [Overview](#31-overview)
   - [Interconnectivity](#32-interconnectivity)
     - [Wide Area Network (WAN) connectivity](#321-wide-area-network-wan-connectivity)
     - [Connectivity among departments](#322-connectivity-among-departments)
     - [Connectivity among devices within the same departments](#323-connectivity-among-devices-within-the-same-departments)
     - [Connectivity among LANS and Internet](#324-connectivity-among-lans-and-internet)
   - [VLAN Segmentation](#33-vlan-segmentation)
   - [External Networks](#34-external-networks)
     - [Demilitarized Zone (DMZ)](#341-demilitarized-zone-dmz)
     - [Teleworker connection](#342-teleworker-connection)
     - [Site-to-site VPN](#343-site-to-site-vpn)
4. [Network System Simulation](#4-network-system-simulation)
   - [Connect between PCs in the same VLAN](#41-connect-between-pcs-in-the-same-vlan)
     - [Connect two PCs inside Operation & Legal department](#411-connect-two-pcs-inside-operation--legal-department)
     - [Connect A PC connected via Ethernet and a laptop connected to Wifi inside Banking department](#412-connect-a-pc-connected-via-ethernet-and-a-laptop-connected-to-wifi-inside-banking-department)
   - [Connect PCs between VLANs](#42-connect-pcs-between-vlans)
     - [Connect a PC from Operation & Legal to a PC in Banking](#421-connect-a-pc-from-operation--legal-to-a-pc-in-banking)
     - [Connect a PC from a HCM department to a server](#422-connect-a-pc-from-a-hcm-department-to-a-server)
   - [Connect PCs between Headquarters and branches](#43-connect-pcs-between-headquarters-and-branches)
     - [Connect PC from HCM to a PC in Hanoi](#431-connect-pc-from-hcm-to-a-pc-in-hanoi)
     - [Connect PC in HANOI to Mail Server in HCM](#432-connect-pc-in-hanoi-to-mail-server-in-hcm)
   - [Connect to servers in the DMZ](#44-connect-to-servers-in-the-dmz)
   - [No connections from Customers’ devices to PCs on the LAN](#45-no-connections-from-customers-devices-to-pcs-on-the-lan)
     - [Cannot connect from Customer laptop to a PC on Floor2](#451-cannot-connect-from-customer-laptop-to-a-pc-on-floor2)
     - [Cannot connect from Customer laptop to a server](#452-cannot-connect-from-customer-laptop-to-a-server)
   - [Connect to the Internet to a Web server](#46-connect-to-the-internet-to-a-web-server)
     - [Connect from PC HCM Floor2 4 to 8.8.8.8](#461-connect-from-pc-hcm-floor2-4-to-8888)
     - [Connect from PC 1 (HANOI) to Web Server using Web Browser via HTTP](#462-connect-from-pc-1-hanoi-to-web-server-using-web-browser-via-http)
   - [Security](#47-security)
     - [Firewall](#471-firewall)
5. [Network Evaluation](#5-network-evaluation)
   - [Security Assessment](#51-security-assessment)
   - [Scalability Assessment](#52-scalability-assessment)
   - [Unresolved Issues](#53-unresolved-issues)
   - [Future Design Directions](#54-future-design-directions)
6. [References](#6-references)

---

## 1. Network Requirements

BB Bank, a company that asked us to design a computer network for, laid out their requirements:

- **The Headquarter:**
  - Located in Ho Chi Minh City.
  - Has 120 workstations, 5 servers and 12 or more networking devices.
- **The Branches:**
  - 1 located in Da Nang, another in Ha Noi.
  - Has 30 workstations, 3 servers and 5 or more networking devices for each branch.
- Usage of new technologies for network infrastructure.
- High security, high availability, robustness when problems occur, ease of upgrading the system.
- A VPN configuration for site-to-site and for a teleworker to connect to Company LAN.
- A surveillance camera system for the Company.
- Connection between Headquarter and Branches by 2 leased lines for WAN connection.
- All traffic to the Internet passes through the Headquarters subnet, with 2 xDSL for Internet access with a load-balancing mechanism.
- The dataflows and workload of the network can be summarized as:
  - Servers for software updates, web access, and database access,... The total download estimate is about 1000 MB/day and the upload estimate is 2000 MB/day for each server.
  - Each workstation is used for Web browsing, document downloads, and customer transactions, ... The total download estimate is about 500 MB/day and the upload estimate is 100 MB/day.
  - WiFi-connected devices from customers’ access for downloading are about 500 MB/day.
  - The system peak at 9AM-11AM and 3PM-4PM, with 80% of dataflows belong to these timeframes.
- Is estimated to have a growth rate of 20% in 5 years (in terms of the number of users, network load, branch extensions,...).

---

## 2. Network Analysis and Design

### 2.1 Analysis of Physical Layout

#### 2.1.1 Overview

The network design should meet the network requirements, with many options suggested along with advantages, disadvantages, and cost. Therefore, we divide the system into smaller parts and focus on analyzing each part.

We begin with survey and design a network layout for the company, then give options for network schematic. Second is the analysis for each equipment and each schematic in general. Thirdly, we calculate throughput and recommend appropriate plans from ISP (Internet Service Provider). Finally, we will design and simulate a specific network layout from the recommended list.

#### 2.1.2 Layout Survey

A survey on the office’s locations should record the following details:

- Physical layout of the buildings:
  - Area for installation of network devices, security devices and peripheral devices.
  - Physical obstacles and interference (building’s electricity, environment’s magnetism,...) that may have adverse effect on network signal traversal.
- Department-specific and room-specific:
  - Expected number of people a room may have.
  - Functionality and security constraints of each room.

#### 2.1.3 Layout Analysis

Assuming that a study upon the BB Bank offices has completed, we got the departments of the Headquarter, 2 Branches and the physical layout of the 3 offices as follows.

A normal work room will have the following installation layout:

- **Departments of BB Bank**
  - Headquarter:
    - Banking: 20 workstations
    - Operations & Legal: 20 workstations
    - Risk Management: 20 workstations
    - Finance: 20 workstations
    - Human Resources: 20 workstations
    - IT: 10 workstations
    - Administration: 10 workstations
  - Branches:
    - Banking: 10 workstations
    - Operations & Legal: 10 workstations
    - IT: 5 workstations
    - Administration: 5 workstations

### 2.2 Network Design

#### 2.2.1 Connection Type

We consider the first pair of options to choose from, which is the connection type of workstations. Firstly, a router (Cisco ISR4331/K9) must be bought for HQ and each branch, along with 4 Ethernet switches (Cisco 4-Port Gigabit Ethernet Switch NIM NIM-ES2-4).

Furthermore, a company using a wired network must also have Wi-Fi access points to accommodate customers and peripheral devices connection.

With wired connection, the newest and most stable technology today is Ethernet-Cat8. Its advantage is that it can offer up to 40Gbps speed and reduce interference, while its principle disadvantage is and the cable is less flexible. We still need 11 switches (Cisco 24 Port Catalyst 2960 WS-C2960-24TC-L) and 11 lightweight Wi-Fi access points (TPLink Archer C54) for 7 floors of HQ 2 floors of each branch.

With wireless connection, we can choose 11 access points of Wi-Fi 6E technology (Cisco CW9162I-MR 802.11ax Wi-Fi 6E 2x2:2 Access Point). This option advantage is its not limited by the number of Ethernet ports while its disadvantage lies in being interference from many workstations trying to access Internet.

Each data with their typical specifications and costs are as follows:

- **Router: Cisco ISR4331/K9**
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

- **Network Interface Card: Cisco 4-Port Gigabit Ethernet Switch NIM NIM-ES2-4**
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

- **Switch: Cisco 24 Port Catalyst 2960 WS-C2960-24TC-L**
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

- **Baseus Cat8 40-Gigabit RJ45 Network Cable**
  - Cost: 400,000 VND/cable of 10 meter
  - Transmission speed: 40 Gbps
  - Bandwidth: 2000 MHz
  - Shielding: 4 layers
  - 30 AWG pure copper wire core
  - 48-strand braided cable jacket

- **Access Point: TPLink Archer C54**
  - Cost: 400,000 VND
  - WiFi:
    - Standard: Wi-Fi 5
    - Speed: 867 Mbps (5 GHz), 300 Mbps (2.4 GHz)
    - Coverage: 3-bedroom apartment, 4× antennas
    - Capacity: Moderate
    - Dual Band: Yes
    - MU-MIMO: 2×2
  - Hardware:
    - Ethernet Ports: 1× WAN, 4× LAN (10/100 Mbps)
  - Security:
    - Wi-Fi Encryption: WPA, WPA2
  - Software:
    - Network Security: SPI Firewall, Access Control
    - Guest Network: 1× 5 GHz, 1× 2.4 GHz

- **Access Point: Cisco CW9162I-MR 802.11ax Wi-Fi 6E 2x2:2 Access Point**
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

#### 2.2.2 Network Security

A security solution can be recommended following the DMZ architecture. A DMZ will contain a Firewall and servers that handle client or outgoing interactions.

- **Firewall: Cisco ASA5506-SEC-BUN-K9**
  - Cost: 25,000,000 VND
  - Throughput: Application Control (AVC)
    - 250 Mbps
  - Throughput: Application Control (AVC) and IPS
    - 125 Mbps
  - Max Concurrent Sessions: 20,000 (50,000 with License)
  - Max New Connections per Second: 5,000
  - Supported Applications: 3,000+
  - URL Categories: 80+
  - Categorized URLs: 280 million+
  - Stateful Inspection Throughput (Max): 750 Mbps
  - Stateful Inspection Throughput (Multiprotocol): 300 Mbps
  - 3DES/AES VPN Throughput: 100 Mbps
  - Users/Nodes: Unlimited

- **Software: Cisco SEC-K9 License**
  - Cost: 27,258,507 VND
  - Purpose: Enhances security on Cisco routers and switches.
  - Key Features:
    - VPN support for secure remote connections.
    - Advanced encryption for data security.
    - Integrated firewall capabilities.
    - Intrusion Prevention System (IPS) for network protection.
    - Content filtering options.

#### 2.2.3 Surveillance and Peripheral System

Another choice for BB Bank is that whether the surveillance and peripheral system is designed upon an Internet of Things (IoT) framework or each independent device handle different functions.

Consider the latter option, we can design a system where surveillance system transmit their data to the IT department over the nearest WiFi access point or router, with peripheral devices like fire monitors, sirens for money storage, are each function independently. The upsides of this system is its independence between devices, not having a single point of failure, cheaper than the other option while its downsides are BB Bank having less ability to control it.

An IoT system can be designed with consideration of BB Bank’s 3 locations physical layout, connected directly into IT department VLAN. The system’s function is to control peripheral devices and surveillance system, itself being controlled by the IT department. Such a system helps BB Bank to have greater control over workspace and can improve performance of the whole system while its downside being more expensive than the previous option, requires expertise in IT department to maintain the system and have single point of failure.

Considering just the surveillance system, a proposal upon the system can be made as follow:

- **Camera: DS-2GN5750-HH**
  - Cost: 4.335,000 VND
  - High-quality imaging with 4 MP resolution
  - Excellent low-light performance
  - Efficient H.265+ compression technology
  - Water and dust resistant (IP67)
  - 24/7 colorful imaging
  - Support Human and Vehicle Detection

#### 2.2.4 Virtual Private Network

A VPN configuration for BB Bank can be assigned upon each department. A proposal for VPN configuration is as follow:

##### 2.2.4.a Site-to-Site VPN Configuration

Below is our requirements for Site-to-Site VPN setup:

- For interconnecting the bank’s main office with its regional branches, a site-to-site VPN will be established. This will use IPSec protocol to ensure secure and encrypted communication between sites.
- Each branch will have a dedicated VPN gateway that will connect to the main office’s central VPN server. This setup will allow seamless sharing of resources and maintain a consistent security posture.
- The VPN will be configured to support dynamic routing protocols like OSPF or BGP to ensure efficient network traffic management.

With that, the solution we choose is Cisco Meraki MX Series:

- Features: Offers integrated SD-WAN and security features. It’s cloud-managed, simplifying complex VPN setups.
- Costs: From 14,500,000 VND for the cheapest model (MX67)

##### 2.2.4.b Teleworker VPN Configuration

Below is our requirements for Teleworker VPN setup:

- Remote employees or teleworkers will be provided with VPN client software that can be installed on their work devices. This client will facilitate a secure connection to the BB Bank’s LAN.
- The teleworker VPN will use SSL/TLS for encryption, offering a balance of strong security and ease of use without the need for additional hardware.
- Multi-factor authentication (MFA) will be implemented to enhance security. This ensures that only authorized personnel can access the bank’s network remotely.

With that, the solution we choose is Cisco AnyConnect Secure Mobility Client:

- Features: Offers unified endpoint compliance, robust network access security, web and roaming protection, network visibility, support for mobile devices, and advanced VPN options for secure and flexible remote connectivity.
- Costs: 100,943,200 VND for the 100 Simultaneous (eDelivery) license for 100 connections.

#### 2.2.5 Virtual Local Area Network

VLANs will be implemented across BB Bank’s network to segment the network into smaller, manageable parts. This segmentation helps in improving performance, enhancing security, and simplifying network management. VLANs effectively segregate traffic from different departments, ensuring operational efficiency and data privacy.

Each department within BB Bank (e.g., Accounting, Human Resources, Customer Service) will have its own VLAN. This approach ensures that the traffic and resources relevant to each department are isolated, thereby reducing unnecessary traffic and enhancing security.

The size of each VLAN should be based upon the number of personnel, which we can only approximate the upper limit, and the functionality of each department.

- **VLAN IP Plan Table**
  - Floor 1: 256 devices, 192.168.10.1/24
  - Operations & Legal: 256 devices, 192.168.20.1/24
  - Banking: 256 devices, 192.168.30.1/24
  - Risk Management: 256 devices, 192.168.40.1/24
  - Human Resources: 256 devices, 192.168.50.1/24
  - Finance: 256 devices, 192.168.60.1/24
  - IT: 256 devices, 192.168.70.1/24
  - Administration: 256 devices, 192.168.80.1/24

---

## 3. Design the Network Map using Packet Tracer

### 3.1 Overview

Included below is the full view of the Packet Tracer implementation.

### 3.2 Interconnectivity

#### 3.2.1 Wide Area Network (WAN) connectivity

The diagram above depicts the Wide Area Network (WAN) connectivity for BB Bank with three branches, utilizing OSPF (Open Shortest Path First) as the routing protocol with Area 0 configuration. OSPF is a routing protocol used within larger networks to distribute IP routing information using link-state algorithm.

- **OSPF Area 0 (Backbone Area):**
  - Routers within this section are part of Area 0, the backbone area of the OSPF networked environments.
  - The other sites (e.g., branches and externals) in the network must connect to Area 0, making it central to OSPF route propagation and ensuring all areas can communicate effectively.
- **The Router-PT HCM Gateway:**
  - Acts as a gateway for Headquarter and is the core router connecting all branch routers.
  - Acts as the point of the connection to other networks, such as the Internet, DMZ area. In other words, Da Nang and Ha Noi branches are to access the rest of the external network or the internet (depicted on the left of this diagram) through this link.
  - The gateway connects to the primary routers of each branch using dedicated leased lines to ensure critical connections and loads.
- **Router-PT HQ/HANOI/DANANG:**
  - The primary routers for each branch that bridge the network between the internal and external sites.
  - Each connects to the internal network of the branch using Copper Straight-Through.

#### 3.2.2 Connectivity among departments

Sits in between the primary routers and the internal network end devices are three Core Switch in all branches:

In this architecture, the core switch acts as a central for each branch’s network. It is responsible for routing and switching traffic efficiently to ensure seamless connectivity across the company’s various departments and services.

Each floor or department within the branches has its own access switch, which connects back to this central core switch, forming a star topology that centralizes network traffic management.

The VLANs span multiple switches using trunk links. Trunk links carry traffic from all VLANs by default between the switches, allowing devices on different VLANs (in this case, workstations on different floors/different departments) to communicate through the Layer 3 device.

A configuration is in place to allow each device to obtain an IP Address through DHCP. For example, the device below on second floor (which is in VLAN 20) obtains the expected ip address within its submask affordance.

Some other devices like IP Camera and Server are assigned a fixed IP address for consistent access.

#### 3.2.3 Connectivity among devices within the same departments

End devices on each floors/departments are connected to a floor-level switch. Allowing each of them to connect with each other.

#### 3.2.4 Connectivity among LANS and Internet

As you can see, local IP addresses have been translated into public IP addresses. For example, in the picture, the IP address of the PC2 on the second floor of Danang branch, which is translated from 172.16.20.11 into 209.165.0.2 (global IP address in the outside interface Serial0/1/1 of the Main Gateway).

### 3.3 VLAN Segmentation

The following section will focus on explaining the setup in HCM Branch as it is the most complex, while those in the Hanoi and Danang branches are similar but in a smaller scale.

The network is logically divided into several VLANs, separating critical servers, user groups, and guest traffic. This segmentation enhances security and traffic management, with inter-VLAN routing handled by layer 3 switches (The ”core switches” mentioned in the section above) to optimize traffic flow.

The core switch is setup to include different VLAN Configuration, as shown in the design in section 2.2.5.

Different switches from each department are connected to different ports on the core switches and they are configured to be assigned different VLAN as shown on the dialog above.

### 3.4 External Networks

The diagram above presents a multi-faceted network with components for internet access, a DMZ for publicly accessible services, and remote site connectivity for a teleworker, all of which are interfaced via the Main Gateway router connected to the WAN area as explained above in section 3.1.2.a.

#### 3.4.1 Demilitarized Zone (DMZ)

In computer networks, a DMZ, or demilitarized zone, is a physical or logical subnet that separates a local area network (LAN) from other untrusted networks – usually, the public internet. DMZs are also known as perimeter networks or screened subnetworks.

Servers and resources in the DMZ are accessible from the internet, but the rest of the internal LAN remains unreachable. This approach provides an additional layer of security to the LAN as it restricts a hacker’s ability to directly access internal servers and data from the internet.

DMZ networks are often used for the following:

- Isolate and keep potential target systems separate from internal networks;
- Reduce and control access to those systems by external users; and
- Host corporate resources to make some of them available to authorized external users.

#### 3.4.2 Teleworker connection

With a VPN, the institution’s inter-office traffic is sent over the public Internet rather than over a physically independent network. But to provide confidentiality, the inter-office traffic is encrypted before it enters the public Internet.

Here the institution consists of a headquarters, 2 branch offices, and a teleworker that typically accesses the Internet from their home. In this VPN, whenever two hosts within headquarters send IP datagrams to each other or whenever two hosts within the branch office want to communicate, they use good-old vanilla IPv4 (that is, without IPsec services). However, when two of the institution’s hosts communicate over a path that traverses the public Internet, the traffic is encrypted before it enters the Internet.

The VPN configuration is:

- Group Name: cisco
- Group Key: Cisco@123
- Host IP (Server IP): 169.113.0.1
- Username: admin
- Password: Admin@123

#### 3.4.3 Site-to-site VPN

After connection between 1 PC in Hanoi and 1 PC in Danang has been established, the VPN tunnel is set to Active mode, so the site-to-site VPN information is displayed in both routers.

---

## 4. Network System Simulation

Several tests are performed to confirm the connectivity as in the requirements. Note that the IPs from PCs of some of the tests below may change from test-to-test due to DHCP.

We are going to use PING test to check for connectivity and TRACERT command to confirm the routes in some tests like Internet connectivity.

### 4.1 Connect between PCs in the same VLAN

#### 4.1.1 Connect two PCs inside Operation & Legal department

A ping test is performed between PC HCM Floor2 4 (192.168.20.15) and PC HCM Floor2 5 (192.168.20.16).

#### 4.1.2 Connect A PC connected via Ethernet and a laptop connected to Wifi inside Banking department

A ping test is performed between PC HCM Floor3 4 (192.168.30.12) and Laptop HCM Floor3 1 (192.168.30.11).

### 4.2 Connect PCs between VLANs

#### 4.2.1 Connect a PC from Operation & Legal to a PC in Banking

A ping test is performed between PC HCM Floor2 4 (192.168.20.15) and PC HCM Floor3 4 (192.168.30.12).

#### 4.2.2 Connect a PC from a HCM department to a server

A ping test is performed between PC HCM Floor2 4 (192.168.20.15) and Server Mail (192.168.10.30).

### 4.3 Connect PCs between Headquarters and branches

#### 4.3.1 Connect PC from HCM to a PC in Hanoi

To verify the connection of PCs between Headquarter and branches, we ping a PC in HANOI branch (172.16.20.11) from a PC in HCM (192.168.20.11).

#### 4.3.2 Connect PC in HANOI to Mail Server in HCM

We also test the connection from a PC in Hanoi (172.16.20.11) to access a mail server (192.168.10.10) in HCM.

### 4.4 Connect to servers in the DMZ

A ping test is performed between PC in HCM branch and a server in the DMZ.

### 4.5 No connections from Customers’ devices to PCs on the LAN

Laptops from customers connected to the Customer WIFI are blocked from access the rest of the network using ACL/Firewall.

#### 4.5.1 Cannot connect from Customer laptop to a PC on Floor2

A ping test is performed between Laptop0 by customer (169.254.42.232) to PC HCM Floor2 4 (192.168.20.13) to confirm there is no connection.

#### 4.5.2 Cannot connect from Customer laptop to a server

A ping test is performed between Laptop0 by customer (192.168.10.12) to Server Mail (192.168.10.30) to confirm there is no connection.

### 4.6 Connect to the Internet to a Web server

#### 4.6.1 Connect from PC HCM Floor2 4 to 8.8.8.8

A ping test and trace route is performed from a PC in HCM to server 8.8.8.8 on the internet to confirm the connection and routing to the internet.

#### 4.6.2 Connect from PC 1 (HANOI) to Web Server using Web Browser via HTTP

Alternatively, we also attempt to use the web browser to access the 8.8.8.8 server on the internet.

### 4.7 Security

In this part, we added a security license called K9 for the router

#### 4.7.1 Firewall

The internal LAN consists of Headquarters and 2 branches which sends traffic to the DMZ and Internet. The DMZ can send and receive traffic from LAN and Internet. The Internet cannot send the traffic to the internal LAN. It is blocked by the firewall and the Intrusion Prevention System (IPS) in the Main Gateway router.

The traffic from ISP server is prevented by the Main Gateway router when it attempts to send ICMP packets to the Mail server in the Headquarters due to firewalls and IPS, which send SYSLOG to the Sys Log server in the IT room.

---

## 5. Network Evaluation

### 5.1 Security Assessment

A company’s system must be robust and secure to protect important information, business strategies, and partner contracts. Therefore, the system must meet certain minimum security requirements such as:

- User access control.
- Early prevention of unauthorized access.
- Immediate alerts when there are unauthorized attempt.

This has been implemented and demonstrated in the section above.

### 5.2 Scalability Assessment

- The system should be designed for easy expansion (adding devices, network cables, etc.) to accommodate the growth needs of the bank, both at the headquarters and its branches.
- Currently, the main headquarters has about 120 workstations spread over 7 floors, each floor having departments with 10-30 workstations. As per the current design, each floor uses 2 24-port switches (excluding one port connected to the main switch), which allow 47 ports, allowing for more devices to be connected as staff numbers increase.

### 5.3 Unresolved Issues

- The system still has many centralized connection points (core switches, core routers), causing system-wide disruptions when these devices fail.
- The design could not be confirmed to meet daily download and upload requirements.
- Being primarily theory-based, the design may not fully align with practical realities.
- The cost of Cisco network devices is high, though reductions are possible in some areas.

### 5.4 Future Design Directions

- Find alternatives to Cisco devices to save cost.
- Design to ensure the network is unclogged, meeting daily system download and upload capacity requirements.
- Thoroughly assess practical needs, equipment costs, and design expenses to create a network that meets both system requirements and cost considerations.
- Implement fail-safe so that a failure in one important node (such as core switch) does not bring down the whole system.

---

## 6. References

1. Jim Kurose and Keith Ross, Computer Networking: A Top-Down Approach (8th edition), PEARSON, 2020
2. Priscilla Oppenheimer, Top-Down Network Design (Third edition), Cisco Press, 2011
