# Project 1 — Virtual SOC Lab Setup (VirtualBox Internal Network)

## Objective
Design and build a fully isolated SOC lab that simulates real-world enterprise environments and supports future Blue Team activities such as SIEM monitoring, alert triage, threat hunting, and incident response.

---

## Lab Architecture Overview
- **Hypervisor:** Oracle VirtualBox  
- **Network Type:** Internal Network  
- **Network Name:** SOC-LAB  
- **Subnet:** 192.168.56.0/24  

This design ensures isolation from the internet, preventing noise and maintaining safe attack containment.

![VirtualBox Internal Network](screenshots/01-virtualbox-internal-network.png)

---

## Virtual Machines & Roles

| VM | Role | IP Address |
|---|---|---|
| Windows 11 | Endpoint (Wazuh Agent – future) | 192.168.56.10 |
| Ubuntu Desktop | SOC / Monitoring (Wazuh / ELK) | 192.168.56.20 |
| Metasploitable 2 | Vulnerable Target | 192.168.56.30 |
| Kali Linux | Attacker / Simulation | 192.168.56.40 |

---

## IP Address Verification

### Windows 11
![Windows IP Config](screenshots/02-windows-ipconfig.png)

### Ubuntu Desktop
![Ubuntu IP](screenshots/04-ubuntu-ip-address.png)

### Metasploitable 2
![Metasploitable IP](screenshots/05-metasploitable-ip-address.png)

### Kali Linux
![Kali IP](screenshots/03-kali-ip-address.png)---

## Connectivity Testing & Troubleshooting

### Initial Connectivity Failure
Inbound ICMP requests to Windows were blocked by Windows Defender Firewall.

![Kali to Windows Ping Failed](screenshots/06-kali-to-windows-ping-failed.png)

---

### Firewall Configuration (Controlled Change)

**Firewall Status Review**
![Windows Firewall Status](screenshots/07-windows-firewall-status.png)

**Inbound ICMP Rule Enabled**
![ICMP Rule Enabled](screenshots/08-windows-firewall-icmp-rule-enabled.png)

---

### Connectivity Restored

**Kali → Windows**
![Kali to Windows Ping Success](screenshots/09-kali-to-windows-ping-success.png)

**Windows → Metasploitable**
![Windows to Metasploitable Ping](screenshots/10-windows-to-metasploitable-ping.png)

**Ubuntu → Kali**
![Ubuntu to Kali Ping](screenshots/11-ubuntu-to-kali-ping.png)

---

## Network Flow Diagram

![SOC Lab Network Diagram](screenshots/12-soc-lab-network-diagram.png)

---

## Key Skills Demonstrated
- Secure lab isolation using internal networks  
- Static IP configuration across Windows & Linux  
- Network troubleshooting and firewall rule management  
- Documentation and structured lab design  
- SOC-oriented thinking and architecture  

---

## Next Steps
- Deploy Wazuh Manager on Ubuntu  
- Install Wazuh Agent on Windows  
- Generate attack telemetry and alerts  
- Perform alert triage and incident response simulations  

