# Homelab Setup

> Personal cybersecurity and networking lab — pfSense firewall, Security Onion SIEM, Elastic Stack v7, and virtualized network environments. Used for security research, certification study, and testing configurations before production deployment.

---

## Lab Overview

```
                        [ Internet ]
                             |
                        [ pfSense ]
                       /     |     \
              [DMZ]  [LAN]  [OPT1]  [Management]
                |      |      |
           [Kali]  [VMs]  [Security Onion]
                              |
                        [Elastic Stack]
                     (SIEM + Log Analysis)
```

---

## Components

### Firewall — pfSense
- Multi-interface setup: WAN, LAN, DMZ, Management VLAN
- Firewall rules and NAT configuration
- VPN (OpenVPN) for remote lab access
- IDS/IPS via Suricata integration
- Traffic shaping and monitoring

### SIEM — Security Onion
- Network security monitoring platform
- Integrated: Zeek, Suricata, Elasticsearch, Kibana
- Full packet capture and analysis
- Alert triage and investigation workflow

### Log Analysis — Elastic Stack v7
- Elasticsearch for log storage and search
- Kibana dashboards for visualization
- Logstash/Beats for log ingestion
- Custom detection rules and alerts

### Virtualization
- VMware Workstation / VMware ESXi
- VirtualBox for lightweight VMs
- VM templates for quick lab resets

---

## Virtual Machines

| VM | OS | Purpose |
|----|-----|---------|
| pfSense | FreeBSD | Firewall/Router |
| Security Onion | Ubuntu | SIEM/NSM |
| Kali Linux | Debian | Attack/Pentest |
| Windows Server | Windows 2019 | AD, DNS, DHCP |
| Ubuntu Server | Ubuntu 22.04 | Web/App server |
| Metasploitable | Linux | Vulnerable target |
| DVWA | Linux | Web app practice |

---

## Network Segments

| Segment | Subnet | Purpose |
|---------|--------|---------|
| LAN | 192.168.1.0/24 | Main lab network |
| DMZ | 192.168.2.0/24 | Exposed services |
| Management | 192.168.100.0/24 | Network devices |
| Attack | 192.168.99.0/24 | Isolated pentest range |

---

## Setup Guides

### pfSense Initial Setup
1. Download pfSense ISO from pfsense.org
2. Install on VM (2 NICs minimum: WAN + LAN)
3. Access web UI at `https://192.168.1.1`
4. Configure interfaces, DHCP, DNS
5. Set up firewall rules per segment
6. Enable Suricata package for IDS

### Security Onion Setup
1. Download Security Onion ISO
2. Install with `Import` mode (for lab — no dedicated sensor)
3. Configure interface connected to pfSense SPAN port
4. Access Kibana/SOC dashboards
5. Tune alert thresholds for lab traffic

### Elastic Stack v7 (Standalone)
```bash
# Install Elasticsearch
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.17.0-amd64.deb
dpkg -i elasticsearch-7.17.0-amd64.deb
systemctl enable --now elasticsearch

# Install Kibana
wget https://artifacts.elastic.co/downloads/kibana/kibana-7.17.0-amd64.deb
dpkg -i kibana-7.17.0-amd64.deb
systemctl enable --now kibana

# Install Filebeat for log shipping
# Configure filebeat.yml with Elasticsearch output
```

---

## Use Cases

- **Certification Study:** CCNA, CCNP, CEH lab exercises
- **Malware Analysis:** Isolated sandbox environment
- **CTF Practice:** Local vulnerable VM challenges
- **Config Testing:** Test network configs before production
- **Detection Engineering:** Write and test SIEM rules
- **Forensics Practice:** Generate artifacts, practice acquisition

---

## Hardware

| Component | Spec |
|-----------|------|
| Host machine | Multi-core CPU (8+ cores recommended) |
| RAM | 32GB+ (16GB minimum) |
| Storage | 500GB+ SSD |
| NICs | 2+ physical NICs for pfSense |
| Hypervisor | VMware ESXi / Workstation / VirtualBox |

---

*Lab environment continuously updated. Used for professional development and research.*
