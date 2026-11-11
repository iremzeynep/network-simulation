# SME Network Design and Implementation

## About the Project

This project is a comprehensive Local Area Network (LAN) simulation designed for Small and Medium-Sized Enterprises (SMEs), with a strong emphasis on service continuity and data security. Developed using Cisco Packet Tracer, this network topology is configured to meet the requirements of modern corporate network architectures.

## Key Features and Technologies

* **VLAN Segmentation (Layer 2):** To isolate network traffic, prevent broadcast storms, and enhance hardware-level security, the network infrastructure is divided into 4 distinct logical units:[cite: 33]
  * `VLAN 10` - Server Farm (Data Center): A high-security zone hosting critical services (Central DHCP, Web, and DNS servers).[cite: 33]
  * `VLAN 20` - Accounting: An operational unit handling sensitive financial and corporate data, requiring strict access control.[cite: 33]
  * `VLAN 30` - Regular Users: The general workforce layer tasked with standard daily business operations.[cite: 33]
  * `VLAN 40` - Guest Network: A completely untrusted and isolated segment reserved for external visitors, strictly prohibited from accessing internal corporate assets.[cite: 33]

* **Inter-VLAN Routing:** A "Router-on-a-Stick" architecture is implemented to enable controlled inter-VLAN routing while maintaining cost efficiency. A single physical router interface is divided into logical sub-interfaces using the IEEE 802.1Q trunking protocol, with each sub-interface acting as the default gateway for its respective VLAN.[cite: 33]

* **Centralized IP Management and DHCP Relay:** IP address allocation across the entire network is automated via a central DHCP server located in the Server Farm. To resolve the architectural limitation where Layer 3 boundaries drop client DHCP broadcast requests, the `ip helper-address` (DHCP Relay Agent) configuration is applied to the router's sub-interfaces. This intercepts broadcast requests and forwards them directly to the central server as unicast packets.[cite: 33]

* **Security Policies (Extended ACLs):** Strict security and isolation policies are enforced at Layer 3 using Extended Access Control Lists (ACLs):[cite: 33]
  * **Guest Network Isolation:** The guest network (VLAN 40) is completely blocked from accessing the Server Farm, Accounting, and Regular User subnets. Essential DHCP operations and standard outbound internet traffic are explicitly permitted.[cite: 33]
  * **Internal Security:** To prevent unauthorized cross-departmental access, traffic originating from the Regular Users subnet (VLAN 30) destined for the sensitive Accounting subnet (VLAN 20) is explicitly denied at the router interface level.[cite: 33]

## Installation and Usage Guide

1. Ensure you have **Cisco Packet Tracer** (v7 or higher) installed on your system.[cite: 33]
2. Clone or download this repository to your local machine.[cite: 33]
3. Open the `network_simulation.pkt` file using Cisco Packet Tracer.[cite: 33]
4. You can click on the network devices to inspect their CLI configurations, including routing tables, ACL rules, and VLAN assignments.[cite: 33]
5. To validate system functionality and security constraints, you can perform ping (ICMP) tests between end devices. For example, attempt to ping the servers from a Guest PC, or the Accounting department from a Regular User PC; you will observe that these unauthorized requests are successfully dropped by the ACLs (resulting in a "Destination host unreachable" message).[cite: 33]
