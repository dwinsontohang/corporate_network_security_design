# CORPORATE NETWORK SECURITY PROJECT #
A well-structured network is critical for ensuring efficient data flow, segmentation, and security while supporting business operations. This corporate network security report details the design, implementation, and security configurations of a scalable network infrastructure, incorporating best practices in routing, VLAN segmentation, and access control.
The network follows a hierarchical architecture, with VLANs ensuring logical segmentation and OSPF routing optimising data flow. DHCP relay, NAT, and static routing are implemented to facilitate communication between internal and external networks. Trunking and port security are enforced at the switch level to prevent unauthorised access.
Security is addressed through Zone-Based Firewall (ZPF), Access Control Lists (ACLs), and AAA authentication (TACACS+), which regulate traffic between security zones and enforce access policies. IPsec VPN tunnels provide secure remote connectivity, allowing encrypted communication between branch and main offices.
The infrastructure is validated through testing and verification of firewall rules, routing protocols, and network policies, ensuring compliance with security standards. This design ensures a resilient, scalable, and cyber-secure network capable of supporting long-term business growth.

## Network Architecture & Infrastructure Design ##
### 1 Network Design ###

**Physical Infrastructure**

The physical infrastructure is structured around a two-tier hierarchical model comprising the Distribution and Access layers, ensuring modularity, scalability, and redundancy for seamless network performance and future expansion.

1. Distribution Layer
   At the core of the network, the Distribution Layer serves as the aggregation point for inter-VLAN communication and traffic routing. The implementation utilises Cisco Catalyst 2960 Switches, known for their high reliability, cost-effectiveness, and efficient Layer 2 switching.

4. Access Layer
   The Access Layer is designed to provide connectivity for end-user devices, ensuring efficient and reliable access to network resources. Each floor is equipped with Cisco Catalyst 2960 Switches, which serve as the primary connection point for:
    * End-user devices such as desktops and laptops
    * Wireless Access Points to provide seamless Wi-Fi coverage
    * Departmental segmentation, ensuring localised traffic management and reduced congestion

Adopting a hierarchical network design brings several important advantages. By segmenting traffic, it helps to minimise congestion and ensure a smoother flow of data across the network. The structured approach makes troubleshooting and maintenance far more straightforward, allowing for quicker fault isolation and easier diagnostics. Security is also significantly improved, as VLAN segmentation at the distribution layer reduces the risk of unauthorised access while enabling more effective policy enforcement. Moreover, the modular nature of this design ensures the network can scale effortlessly, allowing for future expansion without the need for major infrastructure changes.

**Network Topology**

To enhance security and performance, the network is segmented into VLANs, each serving a specific function:

1. Departmental VLANs
   Each department operates within a dedicated VLAN, preventing unnecessary broadcast traffic and ensuring efficient resource allocation:

    * Sales & Marketing – 30 users

    * Development – 50 users

    * IT – 20 users

    * HR – 25 users

    * Finance – 25 users

3. Functional VLANs
   In addition to departmental segmentation, key operational areas have dedicated VLANs to streamline performance and security:

    * Server VLAN – Hosts critical infrastructure such as File, Web, DHCP, and AAA servers.

    * Demilitarised Zone (DMZ) – Isolates external-facing services like the company's web and email servers, providing an additional security layer.

    * Management VLAN – Reserved exclusively for IT administrators to manage network devices securely.


**Network infrastructure and architecture diagram**
<img width="993" height="583" alt="image" src="https://github.com/user-attachments/assets/5b1307e0-f152-427c-b324-ae04402db13e" />


**Logical Topology**
<img width="1147" height="684" alt="image" src="https://github.com/user-attachments/assets/5b98a6ee-0614-4cf3-bb49-76814152e598" />

A star topology provides a centralised approach to network management, allowing for improved traffic flow, simplified troubleshooting, and reduced network downtime. The use of VLAN segmentation ensures that traffic remains isolated where necessary, strengthening security, reducing congestion, and optimising resource allocation. This structured design allows for seamless scalability, enabling the network to adapt effortlessly to future growth and technological advancements.

**Subnetting**

To ensure efficient network segmentation, enhance security, and optimise resource allocation, the 172.16.10.0/24 network has been divided into distinct subnets based on departmental functions and operational needs. Each subnet is assigned a specific IP range to accommodate the required number of devices while minimising wasted address space. This structured approach ensures efficient address management, improved performance, and scalability for future expansion.


**Subnetting for IP allocation**

| No | Department / Function | VLAN | Total Devices | Network Address | Subnet Mask | Broadcast Address | Usable IP Range |
|----|----------------------|------|---------------|-----------------|-------------|-------------------|-----------------|
| 1 | Sales & Marketing | 10 | 30 | 172.16.10.64/27 | 255.255.255.224 | 172.16.10.95 | 172.16.10.65 - 172.16.10.94 |
| 2 | Development | 20 | 50 | 172.16.10.0/26 | 255.255.255.192 | 172.16.10.63 | 172.16.10.1 - 172.16.10.62 |
| 3 | IT | 30 | 20 | 172.16.10.160/27 | 255.255.255.224 | 172.16.10.191 | 172.16.10.161 - 172.16.10.190 |
| 4 | Human Resource | 40 | 25 | 172.16.10.96/27 | 255.255.255.224 | 172.16.10.127 | 172.16.10.97 - 172.16.10.126 |
| 5 | Finance | 50 | 25 | 172.16.10.128/27 | 255.255.255.224 | 172.16.10.159 | 172.16.10.129 - 172.16.10.158 |
| 6 | Conference Room | 60 | 6 | 172.16.10.224/29 | 255.255.255.248 | 172.16.10.231 | 172.16.10.225 - 172.16.10.230 |
| 7 | Server Network | 70 | 5 | 172.16.10.192/28 | 255.255.255.240 | 172.16.10.207 | 172.16.10.193 - 172.16.10.206 |
| 8 | Management Network | 99 | 10 | 172.16.10.208/28 | 255.255.255.240 | 172.16.10.223 | 172.16.10.209 - 172.16.10.222 |
| 9 | DMZ | - | - | 172.16.10.232/29 | 255.255.255.248 | 172.16.10.239 | 172.16.10.233 - 172.16.10.238 |

A well-structured IP addressing scheme optimises address space while ensuring network performance, security, and scalability. Subnets are allocated based on departmental needs, enabling efficient resource distribution. VLANs and subnet segmentation minimise broadcast traffic, enhance security by isolating sensitive data, and simplify management. Dedicated subnets for the DMZ and server network keep external traffic separate, while a management network ensures secure device administration.


### 2 Equipment Selection and Placement ###

**Routers**

The Cisco ISR 4331 is deployed as the ISP router and internet, managing WAN connectivity. Meanwhile, the Cisco 2911 serves as the perimeter or internet-facing router, handling VPN termination, NAT, security enforcement, and traffic filtering between the internal network and external connections.

**Switches**

The Cisco Catalyst 2960-L was chosen for its reliability, cost-effectiveness, and efficient Layer 2 switching, making it ideal for both distribution and access layers. It enables VLAN-based segmentation, reducing broadcast domains while ensuring secure and efficient traffic flow. At the distribution layer, it aggregates access layer traffic, while at the access layer, it connects end-user devices like desktops, laptops, and wireless access points. With QoS for prioritising critical traffic and security features like port security, DHCP snooping, and 802.1X authentication.

**Wireless Access Point**

Access points are installed across the office to provide reliable Wi-Fi, allowing employees to move freely and work from their laptops without being tied to a wired connection.

**Servers**

To meet the company's needs, we've set up six servers, each dedicated to a specific function: email, DHCP and DNS, file sharing, the company profile website, an internal web app, and authentication (AAA server).

### 2 Cabling and Connectivity Standards ###

The network follows structured cabling and connectivity standards to ensure reliable and high-speed communication.
    * Distribution to Access Switches: Fibre optic cabling is recommended for real-world deployment, but UTP straight-through cables are used in Cisco Packet Tracer simulations

    * Access Switch to End-User Devices: Cat 6 UTP cables provide stable and high-performance wired connectivity.

    * Access Points: Operate in full-duplex mode, ensuring efficient and uninterrupted wireless communication throughout the office.

Note: The DMZ switch is directly connected to the main router, bypassing the backbone switch to ensure traffic separation. This design enhances bandwidth and throughput by isolating internal network traffic from the DMZ, which is accessible from both internal users and external sources, including the internet.

### 4 Internet Gateway and Perimeter Security ###

To ensure secure and efficient network communication, the internet gateway and perimeter security are managed through the router. The following techniques are deployed:

    * NAT: Translates internal addresses to public IPs for internet access.

    * Zone-Based Firewall (ZPF): Controls and filters traffic based on security policies.

    * Access Control Lists (ACLs): Restrict and manage traffic flow for added security.

    * Routing: Configured to enable seamless inter-VLAN communication and efficient traffic management.

    * IPSec VPN: Provides a secure, encrypted connection between the main office and branch office for protected data transmission.

### 5 Network Segmentation and Zoning ###

To enforce segmentation and limit lateral movement, the network is structured into logical zones and physical boundaries. These zones define different levels of trust and apply strict access controls to ensure security.

Zones of Trust:

1. Untrusted Zone (Internet)
   * All external traffic enters here.
   * Strict Zone-Based Firewall (ZPF) policies block unauthorised access to internal resources.

2. Semi-Trusted Zone
   * Demilitarised Zone (DMZ) – Isolates externally accessible services from the internal network.

3. Trusted Zones
   * Internal Departments – Segmented using VLANs and ACLs to control access between departments.
   * Server Zone – Protected through micro-segmentation with ACLs to restrict lateral movement.

4. Management Zone
   * Dedicated VLAN 99 for secure network device administration.
   * Accessible only via SSH and TACACS+ to authorised personnel.
   This structured segmentation model strengthens security by containing threats, controlling access, and ensuring efficient network management.
