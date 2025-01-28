# Network Infrastructure

### Overview
This repository documents my **homelab network setup**, highlighting my expertise in **network administration, security, and monitoring**. The setup includes:
- **Cisco Router & Switch:** Core network infrastructure with VLANs, DHCP, and ACLs.
- **Proxmox Virtualization Server:** Hosting various VMs for Windows Server, Splunk, Zabbix, and testing environments.
- **Wi-Fi Access Point** Providing secure wireless access.
- **Monitoring & Logging:** Implemented **Zabbix for SNMP monitoring** and **Splunk for log analysis**.
- **VPN Configuration:** Remote access to Servers and Clients via **Tailscale** .

### Skills Learned

- Understanding of SIEM concepts and practical application.
- Creating Network Toplogies/Diagram
- Linux Installation & Administration
- Wireless Network – Configured AP for seamless Wi-Fi access with VLAN segmentation.
- Proficiency in analyzing and interpreting network logs.
- Ability to generate and recognize attack signatures and patterns.
- Enhanced knowledge of network protocols and security vulnerabilities.
- Installing and configuring Zabbix Server and Agents.
- SNMP-based monitoring for network devices
- Analyzing trends in CPU, memory, and bandwidth usage
- Creating custom dashboards for system health network traffic analysis & using graphing tools to visualize resource utilization trends

### Tools Used

- SPLUNK & ZABBIX - Security Information and Event Management (SIEM) system for network management, log ingestion and analysis.
- Network analysis tools (such as Wireshark) for capturing and examining network traffic.
- Telemetry generation tools to create realistic network traffic and attack scenarios.
- Tailscale - Remote Access VPN
- SNMP Tester
- Lucid Charts & Draw.io

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
### Hardware
| Device             | Model             | Role                               | IP                  |
|-------------------|-------------------|-------------------------------------|---------------------|
| Core Switch       | **TBD**           | VLAN Management                     | Static (Management) |
| LAN Router        | Cisco 1921/K0-04  | Gateway, DHCP Server, Internal LAN  | Static              |
| Proxmox Server    | Dell Optiplex     | Virtualization Host                 | Static              |
| TP-Link Router    | Archer A54        | Wi-Fi Access Point                  | Static              |
| ISP Router        | ISP Router        | WAN Router                          | Static              |

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



# Network Topology
![Network Diagram](https://github.com/Plantlyfe/HOMELAB-/blob/main/Stan%20Homelab%20Topology.png)

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

## **Future Plans**
- Implement **Cisco IPSec** for network access control.
- Expand Splunk dashboards for **threat detection**.
- Test **dynamic routing protocols (OSPF/BGP)**.
- Set up an Ansible Playbook for Network Automation using Python.
- Implement AI-driven network management systems.
- Practice BGP configuration, route optimization, and policy management, to effectively manage network traffic in service provider environments.

📄 [View Future Plans](documentation/future-plans.md)
  
