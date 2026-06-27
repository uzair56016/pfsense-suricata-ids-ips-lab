# pfsense-suricata-ids-ips-lab
Network IDS/IPS lab using pfSense, Suricata, and pfBlockerNG with simulated attack detection and blocking
# Network Intrusion Detection & Prevention Lab — pfSense + Suricata + pfBlockerNG

A hands-on home-lab project simulating a segmented enterprise network protected by an open-source firewall/IDS-IPS stack, with live attack simulation and traffic analysis.

## 🎯 Project Overview

This project builds a realistic two-zone network (WAN/Attacker and LAN/Victim) using VMware Workstation, places **pfSense** as the perimeter firewall/router between the zones, and hardens it with **Suricata** (IDS/IPS) and **pfBlockerNG** (GeoIP & reputation-based blocking). Live attacks are launched from a Kali Linux VM against a Windows victim VM to validate detection, alerting, and prevention.

## 🏗️ Lab Architecture

| Role | VM | Network Placement |
|------|----|-------------------|
| Attacker | Kali Linux | WAN-side interface (simulated external network) |
| Firewall / IDS-IPS | pfSense | Dual-homed: 1 NIC on WAN, 1 NIC on LAN |
| Victim | Windows 10/Server | LAN-side interface (internal network) |

[ Kali Linux Attacker ] --- WAN ---> [ pfSense Firewall ] --- LAN ---> [ Windows Victim ]

Suricata (IDS/IPS)

pfBlockerNG (GeoIP/IP blocking)

Two separate virtual network adapters were configured on pfSense — one bound to the WAN interface (attacker-facing) and one bound to the LAN interface (victim-facing) — to enforce proper traffic segmentation and routing through the firewall.

## 🛠️ Components & Configuration

### 1. pfSense Firewall (Core)
- Configured as the routing/firewall boundary between WAN and LAN zones
- Custom firewall rules defined to control and filter inter-zone traffic

### 2. Suricata (IDS/IPS)
- Installed as a pfSense package and bound to both WAN and LAN interfaces
- Deployed in both detection (IDS) and prevention (IPS) modes
- Custom and community rule sets enabled to detect common attack signatures
- Alerts generated and logged for malicious/suspicious traffic
- IPS mode configured to actively **drop** matched malicious traffic in real time

### 3. pfBlockerNG
- Installed as a pfSense package for reputation and geo-based filtering
- GeoIP blocklists configured to block traffic originating from specific high-risk countries
- Custom IP block rules added for known malicious hosts
- Integrated with pfSense's firewall ruleset to enforce blocks automatically

### 4. Attack Simulation & Validation
- Controlled attacks launched from the Kali Linux VM toward the Windows victim across the segmented network
- Verified that Suricata generated accurate alerts for the simulated attack traffic
- Verified that malicious traffic was actively dropped/blocked by Suricata IPS and pfBlockerNG rules
- Confirmed logs and alerts in the pfSense/Suricata dashboard correlated with the attacks performed

## 📊 Results

- Successfully detected simulated attack traffic via Suricata IDS alerts
- Successfully blocked malicious/geo-flagged traffic using pfBlockerNG before it reached the LAN segment
- Demonstrated full IDS → IPS → block pipeline: **Alert → Drop → Block**
- Validated network segmentation effectiveness in containing attacker-originated traffic

## 🧰 Tools & Technologies

`pfSense` `Suricata` `pfBlockerNG` `Kali Linux` `VMware Workstation` `Windows 10/Server` `Network Segmentation` `IDS/IPS`

## 📚 Key Learnings

- Practical experience deploying and tuning an open-source IDS/IPS stack in a routed environment
- Hands-on understanding of GeoIP/reputation-based filtering as a defense-in-depth layer
- Reinforced concepts of network segmentation, firewall rule design, and traffic inspection
- End-to-end validation methodology: simulate → detect → alert → prevent

## ⚠️ Disclaimer

This project was built entirely within an isolated, local virtual lab environment for educational purposes only. All simulated attacks were performed against systems owned and controlled by the author. No external networks or third-party systems were targeted.

---
*Part of a personal cybersecurity learning portfolio focused on network defense and security monitoring.*
