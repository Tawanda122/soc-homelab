# Project 1 — Virtual SOC Lab Setup (VirtualBox Internal Network)

## Objective
The goal of this project was to design and build a **realistic, isolated SOC lab** that mirrors how security teams safely test, monitor, and investigate activity in enterprise environments.

This lab forms the foundation for future Blue Team projects, including SIEM monitoring, alert triage, threat hunting, and incident response workflows.

---

## Lab Architecture Overview

- **Hypervisor:** Oracle VirtualBox  
- **Network Type:** Internal Network  
- **Network Name:** SOC-LAB  
- **Subnet:** 192.168.56.0/24  

An **Internal Network** was deliberately chosen to:
- Fully isolate lab traffic from the internet
- Prevent external noise from affecting logs and alerts
- Safely contain attack simulations
- Reflect real SOC testing environments where malicious activity is controlled

![VirtualBox Internal Network](screenshots/01-virtualbox-internal-network.png)

---

## Virtual Machines & Roles

Each virtual machine was assigned a **specific SOC-relevant role** to simulate a small enterprise environment.

| VM | Role | IP Address |
|---|---|---|
| Windows 11 | Endpoint (future Wazuh Agent) | 192.168.56.10 |
| Ubuntu Desktop | SOC / Monitoring (Wazuh / ELK) | 192.168.56.20 |
| Metasploitable 2 | Vulnerable Target System | 192.168.56.30 |
| Kali Linux | Attack & Simulation Platform | 192.168.56.40 |

Static IP addresses were used to:
- Ensure predictable log sources
- Avoid DHCP-related inconsistencies
- Reflect how assets are typically documented and monitored in enterprise environments

---

## IP Address Verification

Verifying IP configuration on each host ensured:
- Correct network placement
- No accidental exposure to external networks
- Consistent addressing for future SIEM ingestion

### Windows 11
![Windows IP Config](screenshots/02-windows-ipconfig.png)

### Ubuntu Desktop
![Ubuntu IP](screenshots/04-ubuntu-ip-address.png)

### Metasploitable 2
![Metasploitable IP](screenshots/05-metasploitable-ip-address.png)

### Kali Linux
![Kali IP](screenshots/03-kali-ip-address.png)

---

## Connectivity Testing & Troubleshooting

### Initial Connectivity Failure

During testing, inbound ICMP traffic to the Windows endpoint failed.

This behaviour was expected, as **Windows Defender Firewall blocks inbound ICMP by default**, which mirrors real-world endpoint hardening.

![Kali to Windows Ping Failed](screenshots/06-kali-to-windows-ping-failed.png)

This step demonstrates:
- Awareness of default security controls
- Understanding that connectivity issues often stem from defensive configurations

---

### Firewall Configuration (Controlled Change)

Rather than disabling the firewall, a **specific inbound ICMP rule** was enabled to allow controlled testing while maintaining security posture.

**Firewall Status Review**
![Windows Firewall Status](screenshots/07-windows-firewall-status.png)

**Inbound ICMP Rule Enabled**
![ICMP Rule Enabled](screenshots/08-windows-firewall-icmp-rule-enabled.png)

This reflects real SOC practice:
- Minimal rule changes
- Principle of least privilege
- Awareness of security trade-offs

---

### Connectivity Restored

After the firewall adjustment, connectivity testing was repeated to confirm resolution.

**Kali → Windows**
![Kali to Windows Ping Success](screenshots/09-kali-to-windows-ping-success.png)

**Windows → Metasploitable**
![Windows to Metasploitable Ping](screenshots/10-windows-to-metasploitable-ping.png)

**Ubuntu → Kali**
![Ubuntu to Kali Ping](screenshots/11-ubuntu-to-kali-ping.png)

These tests confirm:
- Full bidirectional communication
- Proper network isolation
- Readiness for attack simulation and detection workflows

---

## Network Flow Diagram

The diagram below illustrates how telemetry flows through the lab:
- Endpoints generate logs
- The SOC system performs detection and alerting
- Attack activity is observed rather than blindly executed

![SOC Lab Network Diagram](screenshots/12-soc-lab-network-diagram.png)

---

## Key Skills Demonstrated

- Secure lab design and isolation
- Static IP configuration and asset awareness
- Network troubleshooting and firewall management
- Security-first decision making
- Clear technical documentation
- SOC-oriented architectural thinking

---

## Next Steps

- Deploy Wazuh Manager on Ubuntu
- Install Wazuh Agent on Windows
- Generate attack telemetry from Kali and Metasploitable
- Perform alert triage and incident response simulations

