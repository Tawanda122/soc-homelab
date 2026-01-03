# Project 1 — Virtual SOC Lab Setup (VirtualBox Internal Network)

## Goal
Build a safe, isolated virtual lab that simulates a real SOC environment and supports future projects (Wazuh/ELK, alert triage, threat hunting, incident response).

## Lab Design
- **Hypervisor:** VirtualBox
- **Network Type:** Internal Network (isolated)
- **Network Name:** SOC-LAB
- **Subnet:** 192.168.56.0/24

✅ This prevents internet “noise” and keeps attack activity contained.

![Internal Network](screenshots/01-virtualbox-internal-network.png)

## Virtual Machines
| VM | Role | IP |
|---|---|---|
| Windows 11 | Endpoint (Wazuh Agent later) | 192.168.56.10 |
| Ubuntu Desktop | SOC / Monitoring (Wazuh/ELK later) | 192.168.56.20 |
| Metasploitable 2 | Vulnerable target | 192.168.56.30 |
| Kali Linux | Attacker / Simulation | 192.168.56.40 |

## IP Configuration Evidence
- Windows IP config  
  ![Windows IP](screenshots/02-windows-ipconfig.png)

- Ubuntu IP  
  ![Ubuntu IP](screenshots/03-ubuntu-ip-a.png)

- Kali IP  
  ![Kali IP](screenshots/04-kali-ip-a.png)

- Metasploitable IP  
  ![Meta IP](screenshots/05-metasploitable-ip-a.png)

## Connectivity Testing (ICMP)
### Initial issue (Windows inbound ping blocked)
(Include this if you have it)
![Ping failed](screenshots/06-windows-ping-failed.png)

### Fix: Windows Defender Firewall inbound ICMP rule
- Firewall status / rules view  
  ![Firewall status](screenshots/07-windows-firewall-status.png)

- Enabled inbound ICMP rule  
  ![ICMP rule](screenshots/08-windows-firewall-icmp-rule.png)

### Verified connectivity after fix
- Windows ↔ Metasploitable (success)  
  ![Windows ping success](screenshots/09-windows-ping-success.png)

- Metasploitable → Windows (success)  
  ![Meta ping success](screenshots/10-metasploitable-ping-success.png)

- Kali → Windows (success)  
  ![Kali ping success](screenshots/11-kali-ping-success.png)

## Network Diagram
![Diagram](screenshots/12-network-diagram.png)

## What I Learned
- How to isolate a lab safely using VirtualBox Internal Networks
- Static IP configuration across Windows and Linux VMs
- Troubleshooting connectivity issues (host-only/internal networking + firewall)
- Making controlled security changes (enabling ICMP inbound rule intentionally)

## Next Steps (Project 2)
- Deploy **Wazuh** on Ubuntu
- Install and enrol **Wazuh Agent** on Windows
- Generate events (failed logons / PowerShell activity) and confirm detections
