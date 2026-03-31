# Enterprise Network Segmentation and Defense Lab

## Overview
This project simulates a small enterprise network built in Cisco Packet Tracer with security-focused segmentation and access control. Multiple departments are separated into distinct VLANs, inter-VLAN routing is configured through router-on-a-stick, and Access Control Lists (ACLs) are used to enforce communication restrictions between networks.

The goal of this lab was to design a network that reflects real-world security principles such as least privilege, network segmentation, management plane protection, DMZ isolation, secure remote administration, and switch hardening.

## Objectives
- Segment departments using VLANs
- Configure inter-VLAN routing
- Restrict traffic using ACLs
- Protect a management VLAN
- Isolate a DMZ web server
- Secure administrative access with SSH
- Harden switch ports with port security

## Network Architecture

![Network Topology](topology/network-topology.jpeg)

The network is divided into the following logical segments:

- **HR (VLAN 10):** 192.168.10.0/24
- **Finance (VLAN 20):** 192.168.20.0/24
- **IT (VLAN 30):** 192.168.30.0/24
- **DMZ (VLAN 40):** 192.168.40.0/24
- **Management (VLAN 99):** 192.168.99.0/24

## Technologies Used
- Cisco Packet Tracer
- VLANs
- Router-on-a-Stick
- Access Control Lists (ACLs)
- SSH
- Port Security
- Basic enterprise network design principles

## VLAN Configuration
Each department was placed into its own VLAN to create separate broadcast domains and prevent unrestricted communication at Layer 2.

![VLAN Table](screenshots/vlan/vlan-table.jpeg)

This segmentation provides the foundation for controlling traffic between departments through the router rather than allowing open internal communication.

## Inter-VLAN Routing
Inter-VLAN routing was implemented using router-on-a-stick. Subinterfaces on the router were assigned to each VLAN and configured with 802.1Q encapsulation.

![Inter-VLAN Routing](screenshots/routing/inter-vlan-success.jpeg)

This allowed routed communication between VLANs while still supporting policy enforcement through ACLs.

## Access Control Lists (ACLs)
ACLs were configured to enforce access restrictions across the network. These rules were used to block unauthorized communication while allowing legitimate administrative access.

The implemented policies included:
- HR blocked from accessing Finance
- IT allowed to access protected networks
- Restricted access to the Management VLAN
- Limited traffic to the DMZ

![ACL Rules](screenshots/acl/acl-rules.jpeg)

## Security Validation

### HR Blocked from Finance
Traffic from the HR VLAN to the Finance VLAN was denied to prevent unauthorized access to sensitive financial resources.

![HR Blocked from Finance](screenshots/testing/hr-blocked-finance.jpeg)

### IT Allowed to Access Finance
The IT VLAN retained authorized access, demonstrating role-based network privileges.

![IT Allowed to Access Finance](screenshots/testing/it-allowed-finance.jpeg)


#### Unauthorized Access Blocked
![Management Access Blocked](screenshots/testing/mgmt-blocked.jpeg)

## DMZ Security
A DMZ network was created to host a public-facing web server while limiting unnecessary access.

### HTTP Access Allowed
The DMZ web service was reachable over HTTP as intended.

![DMZ HTTP Access](screenshots/testing/dmz-http-success.jpeg)

## Secure Remote Administration
SSH was configured for secure administrative access to the router. This replaces insecure remote management methods such as Telnet and ensures encrypted login sessions.

![SSH Login](screenshots/ssh/ssh-login.jpeg)

## Network Hardening

### Port Security
Port security was configured on switch access ports to help prevent unauthorized devices from connecting to the network.

![Port Security](screenshots/security/port-security.jpeg)

This hardening included:
- Limiting the number of devices per port
- Sticky MAC address learning
- Automatic shutdown on violation

## Configuration Files
The full device configurations are stored in the repository for reference and review:

- `configurations/router-config.txt`
- `configurations/switch-config.txt`



Key Takeaways

This project demonstrates practical knowledge of:

VLAN-based network segmentation
Inter-VLAN routing with router-on-a-stick
Access control using ACLs
Management plane protection
DMZ design for public-facing services
Secure remote administration with SSH
Switch hardening through port security


Conclusion

This lab reflects how enterprise networks are designed to reduce attack surface, limit lateral movement, and protect sensitive systems through layered security controls. It combines core networking concepts with practical security enforcement and provides a strong hands-on example of entry-level network security engineering work.
