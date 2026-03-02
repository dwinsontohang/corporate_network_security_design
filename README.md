A well-structured network is critical for ensuring efficient data flow, segmentation, and security while supporting business operations. This corporate network security project report details the design, implementation, and security configurations of a scalable network infrastructure, incorporating best practices in routing, VLAN segmentation, and access control.
The network follows a hierarchical architecture, with VLANs ensuring logical segmentation and OSPF routing optimising data flow. DHCP relay, NAT, and static routing are implemented to facilitate communication between internal and external networks. Trunking and port security are enforced at the switch level to prevent unauthorised access.
Security is addressed through Zone-Based Firewall (ZPF), Access Control Lists (ACLs), and AAA authentication (TACACS+), which regulate traffic between security zones and enforce access policies. IPsec VPN tunnels provide secure remote connectivity, allowing encrypted communication between branch and main offices.
The infrastructure is validated through testing and verification of firewall rules, routing protocols, and network policies, ensuring compliance with security standards. This design ensures a resilient, scalable, and cyber-secure network capable of supporting long-term business growth.

**Network Architecture & Infrastructure Design**
***Network Design***
1. Physical Infrastructure 
The physical infrastructure is structured around a two-tier hierarchical model comprising the Distribution and Access layers, ensuring modularity, scalability, and redundancy for seamless network performance and future expansion.
a. Distribution Layer
At the core of the network, the Distribution Layer serves as the aggregation point for inter-VLAN communication and traffic routing. The implementation utilises Cisco Catalyst 2960 Switches, known for their high reliability, cost-effectiveness, and efficient Layer 2.
b. Access Layer
The Access Layer is designed to provide connectivity for end-user devices, ensuring efficient and reliable access to network resources. Each floor is equipped with Cisco Catalyst 2960 Switches, which serve as the primary connection point for:
• End-user devices such as desktops and laptops
• Wireless Access Points to provide seamless Wi-Fi coverage
• Departmental segmentation, ensuring localised traffic management and reduced congestion
Adopting a hierarchical network design brings several important advantages. By segmenting traffic, it helps to minimise congestion and ensure a smoother flow of data across the network. The structured approach makes troubleshooting and maintenance far more straightforward, allowing for quicker fault isolation and easier diagnostics. Security is also significantly improved, as VLAN segmentation at the distribution layer reduces the risk of unauthorised access while enabling more effective policy enforcement. Moreover, the modular nature of this design ensures the network can scale effortlessly, allowing for future expansion without the need for major infrastructure changes.
