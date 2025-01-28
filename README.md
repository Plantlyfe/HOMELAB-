### Overview
Designed, deployed, and maintained a scalable LAN network for multiple devices/users to simulate an enterprise network using a variety of network devices such as a Cisco router, Cisco switch, Access Point and a Proxmox virtualization server. Configured inter-VLAN routing with ROAS. Implemented VLAN segmentation, and optimized Layer 2/3 switching for security and performance such as SNMPv3 for secure enterprise-leve network monitoring. ACL/firewall rules to restrict and permit access. Setup VPN & Remote Access for secure remote administration.

# Network Infrastructure

### Overview
This repository documents my **homelab network setup**, highlighting my expertise in **network administration, security, and monitoring**. The setup includes:
- **Cisco Router & Switch:** Core network infrastructure with VLANs, DHCP, ACLs, and VPN.
- **Proxmox Virtualization Server:** Hosting various VMs for Windows Server, Splunk, Zabbix, and testing environments.
- **Wi-Fi Access Point** Providing secure wireless access.
- **Monitoring & Logging:** Implemented **Zabbix for SNMP monitoring** and **Splunk for log analysis**.
- **VPN Configuration:** Remote access via **Tailscale**.

### Skills Learned

- Advanced understanding of SIEM concepts and practical application.
- Proficiency in analyzing and interpreting network logs.
- Ability to generate and recognize attack signatures and patterns.
- Enhanced knowledge of network protocols and security vulnerabilities.
- Development of critical thinking and problem-solving skills in cybersecurity.

### Tools Used

- SPLUNK & ZABBIX - Security Information and Event Management (SIEM) system for network management, log ingestion and analysis.
- Network analysis tools (such as Wireshark) for capturing and examining network traffic.
- Telemetry generation tools to create realistic network traffic and attack scenarios.
- Tailscale - Remote Access via VPN

###  **Firewall Rules & Security** 
| Purpose                                        | Destina                   | Purpose        |
|-----------------------------------------------|----------------------------|----------------|
| Management                                    | Network Admins              | Network Admins|
| Servers                                       | test                        | Network Admins|
| Workstation                                   | test                        | Network Admins|
| Access Point                                  | Wifi                        | Network Admins|

- Configured **ACLs** on Cisco Router to restrict access between VLANs and to provide Internet Access via ISP.

📄 [View ACL Rules](firewall/acl-rules.md)


### **VLAN Configuration/ Subnet Plan**
| VLAN Name         | Subnet        | Purpose                               |
|-------------------|---------------|---------------------------------------|
| Native VLAN       | Subnet 1      | General Network                       |
| Servers           | Subnet 2      | Windows Server, Zabbix, Splunk        |
| Clients           | Subnet 3      | Windows/Linux Workstations            |
| Access Point      | Subnet 4      | Wi-Fi                                 |
| Managenment       | Subnet 5      | Network Admin                         |



## Steps
drag & drop screenshots here or use imgur and reference them using imgsrc

Every screenshot should have some text explaining what the screenshot is about.

Example below.

*Ref 1: Network Diagram*


## CUT OFF

---

## **Network Topology**
![Network Diagram](topology/network-diagram.png)

---
### Hardware
| Device             | Model             | Role                               | IP                  |
|-------------------|-------------------|-------------------------------------|---------------------|
| Core Switch       | **TBD**           | VLAN Management                     | Static (Management) |
| LAN Router        | Cisco 1921/K0-04  | Gateway, DHCP Server, Internal LAN  | Static              |
| Proxmox Server    | Dell Optiplex     | Virtualization Host                 | Static              |
| TP-Link Router    | Archer A54        | Wi-Fi Access Point                  | Static              |


### Virtual Machines
| VM Name            | OS                     | Role                       | IP           |
|--------------------|------------------------|----------------------------|--------------|
| SPLUNK             | Ubuntu Server          | Syslog Server              | Static       |
| SERVER1            | Windows Server 2022    | Domain Controller          | Static       |
| Target-PC          | Windows 10 Pro         | Client                     | DHCP         |
| Ubuntu Desktop     | Ubuntu Desktop         | Client                     | DHCP         |
| Kali Linux         | Linux                  | Client                     | DHCP         |
| Zabbix             | Ubuntu Server          | SNMP Server                | Static       |
| AdGuard            | Container              | DNS resolver               | DHCP         |
| CML                | Linux                  | Virtual Lab Environment    | DHCP         |

## **Configuration Files**
### **Cisco Router Configuration**
- VLAN configuration with ROAS (Router on a Stick)
- DHCP server setup for each VLAN
- ACLs for security
- VPN setup

📄 [View Configuration](configurations/cisco-router-config.txt)

### **Cisco Switch Configuration**
- VLAN assignments for different devices
- Trunk and access port settings
- STP configuration

📄 [View Configuration](configurations/cisco-switch-config.txt)

---

## **Network Monitoring**
### **Zabbix for SNMP Monitoring**
- Monitoring **CPU, memory, bandwidth usage** for all network devices.
- Custom **Zabbix dashboards** for real-time insights.

📄 [View Zabbix Setup](monitoring/zabbix-setup.md)

### **Splunk for Log Analysis**
- Collecting logs from **Cisco devices, Windows Server, and Linux VMs**.
- Creating dashboards for **failed login attempts, VPN connections, and network activity**.

📄 [View Splunk Setup](monitoring/splunk-setup.md)

---

## **Future Plans**
- Implement **Cisco IPSec** for network access control.
- Expand Splunk dashboards for **threat detection**.
- Test **dynamic routing protocols (OSPF/BGP)**.
- Set up an Ansible Playbook for Network Automation using Python.
- Implement AI-driven network management systems.
- Practice BGP configuration, route optimization, and policy management, to effectively manage network traffic in service provider environments.

📄 [View Future Plans](documentation/future-plans.md)
  
