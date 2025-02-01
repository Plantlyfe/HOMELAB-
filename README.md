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

### Tools Used

- SPLUNK & ZABBIX - Security Information and Event Management (SIEM) system for network management, log ingestion and analysis.
- Network analysis tools (such as Wireshark) for capturing and examining network traffic.
- Telemetry generation tools to create realistic network traffic and attack scenarios.
- Tailscale - Remote Access VPN
- SNMP Paessler Tester Tool
- Lucid Charts & Draw.io for Network diagrams


# Network Diagram
![Network Diagram](https://github.com/Plantlyfe/HOMELAB-/blob/main/Stan%20Homelab%20Topology.png)


### **VLAN Configuration/ Subnet Plan**
| VLAN Name         | Subnet        | Purpose                               |
|-------------------|---------------|---------------------------------------|
| Native VLAN       | Subnet 1      | General Network                       |
| Servers           | Subnet 2      | Windows Server, Zabbix, Splunk        |
| Clients           | Subnet 3      | Windows/Linux Workstations            |
| Access Point      | Subnet 4      | Wi-Fi                                 |
| Managenment       | Subnet 5      | Network Admin                         |

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
| CML                | Linux                  | Virtual Lab Environment    | DHCP         |



## **Configuration Files**
### **Cisco Router Configuration**
- VLAN configuration with ROAS (Router on a Stick)
- DHCP server setup for each VLAN
- ACLs for security and Internet Access

📄 [View Configuration](configurations/cisco-router-config.txt)

### **Cisco Switch Configuration**
- VLAN assignments for different devices
- Trunk and access port settings

📄 [View Configuration](configurations/cisco-switch-config.txt)

---

## **Future Plans**
- Implement site to site VPN to an Oracle Cloud VM via **Cisco IPSec Tunnel** for network access control
- Expand Splunk dashboards for **threat detection**.
- Learn Python and set up an Ansible Playbook for Network Automation.
- Implement AI-driven network management systems (ex. ML for anomaly detection, predicting network issues, or detect zero-day attacks)
- Test & Practice BGP configuration, route optimization, and policy management, to effectively manage network traffic in service provider environments.

📄 [View Future Plans](documentation/future-plans.md)
  
