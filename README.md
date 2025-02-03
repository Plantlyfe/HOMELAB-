# Network Infrastructure

### Overview
This repository documents my **homelab network setup**, highlighting my expertise in **network administration, security, and monitoring**. The setup includes:
- **Cisco Router & Switch:** Core network infrastructure with VLANs, DHCP, and ACLs.
- **Proxmox Virtualization Server:** Hosting various VMs for Windows Server, Splunk, Zabbix, and testing environments such as Cisco Modeling Labs (CML).
- **Wi-Fi Access Point** Providing secure wireless access.
- **Monitoring & Logging:** Implemented **Zabbix for SNMP monitoring** and **Splunk for Syslog analysis**.
- **VPN Configuration:** Remote access to Servers and Clients via **Tailscale** .

### Skills Learned

- Understanding of Security Information and Event Management (SIEM) concepts and practical application (Zabbix & Splunk).
- Creating Network Toplogies/Diagram
- Linux Installation & Administration
- Wireless Network – Configured AP for seamless Wi-Fi access with VLAN segmentation.
- Proficiency in analyzing and interpreting network logs.
- Ability to generate and recognize attack signatures and patterns.
- Enhanced knowledge of network protocols and security vulnerabilities.
- SNMP-based monitoring for network devices
- Analyzing trends in CPU, memory, and bandwidth usage
- Creating custom dashboards for system health network traffic analysis & using graphing tools to visualize resource utilization trends
- SSH Configuration for Remote Access Administration


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

### Firewall / ACL Configuration
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

## Proxmox Server 
![Proxmox](https://github.com/Plantlyfe/Network-Infrastructure/blob/main/proxmox-full-lockup-color.png)

- Downloaded the Proxmox ISO and copied to a USB. Started the automatic installation on a Dell OptiPlex 5070 Micro PC and set static IP outside DHCP Range.
- VM & Container Management accessed through a Web GUI. 
- Installed various Virtual Machines by uploading the ISO into Proxmox to start the installation 
- Tailscale VPN installed via the Proxmox Shell for remote access over the internet.
- Tailscale also installed individually on a few VMs such as SERVER1 & Target-PC for direct remote access.

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
### **Cisco Router (R1) Configuration**
- Accessed the CLI via PuTTY using a Console Connection. Had issue gaining access as the router came in preconfigured with an unknown password required to enter the CLI. 
- Rebooted the router into Rommmon mode (This step bypasses the startup configuration where the passwords are stored) and set the configuration register to 0x2142 to reset router configuration allowing me to set my own username and password.
- Static IP address configured on both my ISP Network & Homelab Network, both outside the DHCP Range to avoid IP conflicts.
- Default Gateway & IP Routes configured to route traffic between VLANs and to ISP/Internet
- VLAN configuration with ROAS (Router on a Stick) for each VLAN.
- DHCP server setup for each VLAN. DHCP addresses excluded in each DHCP pool to allow for static IP configuration
- ACLs for security and Internet Access.
- SNMPv3 Configuration to allow Network Monitoring via Zabbix Server
- Syslog configured to send traps to Splunk Server
- Setup as a DNS relay agent that forwards DNS requests from clients to ISP router.
- Setup plantlyfe domain & configured SSH for remote administration

---

### **Cisco Switch (SW1) Configuration**
- Accessed the CLI via PuTTY using a Console Connection.
- Static IP address configured on Management VLAN for remote SSH Access.
- VLAN assignments for different roles: Server, Client, Access Point, & Management
- Trunk ports configured between SW1 and R1 connection as well as Proxmox and SW1 Connections. TP-Link Router connection configured as access port.
- Subinterfaces configured on both Proxmox and R1 to allow VLAN Hopping
- SNMPv3 configured to allow Network Monitoring via Zabbix Server
- Syslog configured to send traps to Splunk Server
- Setup plantlyfe domain & configured SSH for remote administration
---

### **TP-Link Router (Access Point) Configuration**
- Set router to Accesss Point mode to provide wireless connection to wired homelab network.
- Configured IP addresss to match Access Point VLAN Subnet (outside DHCP range)
- DNS inquires redirected to R1. Turned off DHCP server fuction.
- Performed Ping test to confrim connectivity with different devices in the planylyfe domain.
- Setup allows for wireless administration & SSH connections into plantlyfe domain network devices & servers.

## **Future Plans**
- Introduce **Firewall** Technologies such **Fortigate** or **pfSense** into infrastrucutre for extra layer of security.
- Implement site to site VPN to an Oracle Cloud VM via **Cisco IPSec Tunnel** for network access control
- Expand Splunk dashboards for **threat detection**.
- Learn **Python** and set up an Ansible Playbook for Network Automation.
- Implement AI-driven network management systems (ex. ML for anomaly detection, predicting network issues, or detect zero-day attacks)
- Test & Practice BGP configuration, route optimization, and policy management, to effectively manage network traffic in service provider environments.

📄 [View Future Plans](documentation/future-plans.md)
  
