# Network Infrastructure

### Overview
This repository documents my **homelab network setup**, highlighting my expertise in **network administration, security, and monitoring**. The setup includes:
- **Cisco Router & Switch:** Core network infrastructure with VLANs, DHCP, and ACLs.
- **Proxmox Virtualization Server:** Hosting various VMs for Windows Server, Splunk, Zabbix, and testing environments such as Cisco Modeling Labs.
- **Wi-Fi Access Point** Providing secure wireless access.
- **Monitoring & Logging:** Implemented **Zabbix for SNMP monitoring** and **Splunk for Syslog analysis**.
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
- SSH Configuration for Remote Access Administration

### Tools Used

- SPLUNK & ZABBIX - Security Information and Event Management (SIEM) system for network management, log ingestion and analysis.
- Network analysis tools (such as Wireshark) for capturing and examining network traffic.
- Telemetry generation tools to create realistic network traffic and attack scenarios.
- Tailscale - Remote Access VPN - Intalled on Client PCs and Servers for Remote Access Administration
- SNMP Paessler Tester Tool
- Lucid Charts & Draw.io for Network diagrams


# Network Diagram
![Network Diagram](https://github.com/Plantlyfe/HOMELAB-/blob/main/Stan%20Homelab%20Topology.png)


### **VLAN Configuration/ Subnet Plan**
| VLAN Name         | Subnet                | Purpose                               |
|-------------------|-----------------------|---------------------------------------|
| Native VLAN       | Subnet 1 /24 Mask     | General Network                       |
| Servers           | Subnet 2 /28 Mask     | Windows Server, Zabbix, Splunk        |
| Clients           | Subnet 3 /24 Mask     | Windows/Linux Workstations            |
| Access Point      | Subnet 4 /24 Mask     | Wi-Fi                                 |
| Management        | Subnet 5 /30 Mask     | Network Admin                         |

---

### Firewall / ACL Confiuration
- Access Group Configured to translate IP address via PAT (NAT Overload) on homelab network to access Internet via the ISP Router.
- Blocked Specific Servers access to the internet
- Denied SSH & RDP (Remote Desktop Protocol) access from Client VLAN to Servers VLAN.
- Allowed only specific hosts access to Management VLAN
- Blocked Access Point VLAN from accessing the Management & Server VLANs except for my Admin Laptop
- Example:

`ip access-list extended AP_TO_SERVER`

`remark Block Access Point VLAN from Accessing Server VLAN except for Admin Laptop`

`permit ip host X.X.X.X X.X.X.0 0.0.0.240   ! Allow My Admin PC to access Server VLAN`

`deny ip X.X.X.0 0.0.0.255 X.X.X.0 0.0.0.240  ! Block other Access Point PCs`

`permit ip any any                                ! Allow other traffic`

---
### Hardware
| Device             | Model             | Role                               | IP                  |
|-------------------|-------------------|-------------------------------------|---------------------|
| Core Switch       | Cisco Catalyst WS-C3560-24TS-E 24-Port     | VLAN Management                     | Static (Management) |
| LAN Router        | Cisco 1921/K9-V04  | Gateway, DHCP Server, Internal LAN  | Static              |
| Proxmox Server    | Dell Optiplex     | Virtualization Host                 | Static              |
| TP-Link Router    | Archer A54        | Wi-Fi Access Point                  | Static              |
| ISP Router        | ISP Router        | WAN Router                          | Static              |

![Network Devices](https://github.com/Plantlyfe/HOMELAB-/blob/main/Network%20Devices.jpg)


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
| Cisco Modeling Labs                | Linux                  | Virtual Lab Environment    | DHCP         |



## **Network Device Configuration Files**
### **Cisco Router Configuration**
- Static IP configured to seperate ISP Network & Homelab Network.
- Default gateway and IP Routes configured to route traffic between VLANs and to ISP/Internet
- VLAN configuration with ROAS (Router on a Stick) for each VLAN.
- DHCP server setup for each VLAN. DHCP addresses excluded in each DHCP pool to allow for static IP configuration
- ACLs for security and Internet Access.
- SNMPv3 Configuration to allow Network Monitoring via Zabbix Server
- Syslog configured to send traps to Splunk Server
- Setup as a DNS relay agent to ISP router

---

### **Cisco Switch Configuration**
- Static IP address for configuration.
- VLAN assignments for different roles: Server, Client, Access Point, & Management
- Trunk ports configured between SW1 and R1 connection as well as Proxmox and SW1 Connections.
- Subinterfaces configured on both Proxmox and R1 to allow VLAN Hopping
- SNMPv3 configured to allow Network Monitoring via Zabbix Server
- Syslog configured to send traps to Splunk Server

---

### **TP-Link Router Configuration**
- Configured IP addresss to match Access Point VLAN

## **Future Plans**
- Introduce **Firewall** Technologies such **Fortigate** or **PFsense** into infrastrucutre extra layer of security.
- Implement site to site VPN to an Oracle Cloud VM via **Cisco IPSec Tunnel** for network access control
- Expand Splunk dashboards for **threat detection**.
- Learn **Python** and set up an Ansible Playbook for Network Automation.
- Implement AI-driven network management systems (ex. ML for anomaly detection, predicting network issues, or detect zero-day attacks)
- Test & Practice BGP configuration, route optimization, and policy management, to effectively manage network traffic in service provider environments.

📄 [View Future Plans](documentation/future-plans.md)
  
