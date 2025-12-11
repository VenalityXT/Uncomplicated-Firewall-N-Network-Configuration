# **Network & Firewall Configuration (UFW)**

[![Linux](https://img.shields.io/badge/OS-Linux-blue?logo=linux)](https://www.linux.org/)
[![UFW](https://img.shields.io/badge/Firewall-UFW-blueviolet)](https://wiki.ubuntu.com/UncomplicatedFirewall)
[![Bash](https://img.shields.io/badge/Shell-Bash-green?logo=gnubash)](https://www.gnu.org/software/bash/)
[![Security](https://img.shields.io/badge/Focus-Network%20Security-red)](https://en.wikipedia.org/wiki/Network_security)
[![IPv4](https://img.shields.io/badge/Protocol-IPv4-blue)](https://datatracker.ietf.org/doc/html/rfc791)
[![IPv6](https://img.shields.io/badge/Protocol-IPv6-darkgreen)](https://datatracker.ietf.org/wg/ipv6/)

---

## <span style="color:#2b6cb0">Executive Summary</span>

> This project demonstrates secure network configuration and firewall management on a Linux host using **UFW (Uncomplicated Firewall)**.  
> It showcases foundational firewall concepts—default policies, rule creation, IPv4/IPv6 management, ICMP behavior, logging, and troubleshooting—mirroring real-world junior sysadmin and security operations responsibilities.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Why This Project Matters](#why-this-project-matters)
- [Technologies Used](#technologies-used)
- [Objectives](#objectives)
- [Key Achievements](#key-achievements)
- [Skills Demonstrated](#skills-demonstrated)
- [Firewall Configuration Walkthrough](#firewall-configuration-walkthrough)
  - [Step 1: Verify Firewall Status](#step-1-verify-firewall-status)
  - [Step 2: Configure Default Policies](#step-2-configure-default-policies)
  - [Step 3: Allow Specific Services](#step-3-allow-specific-services)
  - [Step 4: Verify Connectivity](#step-4-verify-connectivity)
  - [Step 5: Enable Firewall Logging](#step-5-enable-firewall-logging)
  - [Step 6: Verify Final Configuration](#step-6-verify-final-configuration)
  - [Step 7: Manage Rules Dynamically](#step-7-manage-rules-dynamically)
- [Key Takeaways](#key-takeaways)
- [Recommendations for Future Enhancements](#recommendations-for-future-enhancements)

---

## <span style="color:#2b6cb0">Project Overview</span>

This project demonstrates how to configure and manage the **UFW firewall** on Linux to enforce secure inbound and outbound traffic policies.  

The configuration steps reflect core system administration tasks:

- Setting default deny/allow rules  
- Opening only necessary services  
- Managing IPv4 and IPv6 rule sets  
- Implementing logging for visibility  
- Validating rule behavior through testing  

These steps build foundational knowledge for secure Linux system hardening.

---

## <span style="color:#2b6cb0">Why This Project Matters</span>

- Reinforces secure system configuration principles  
- Demonstrates least-privilege network access  
- Highlights differences between IPv4 and IPv6 firewall behavior  
- Shows practical firewall rule creation, deletion, and testing  
- Builds confidence in using UFW for real-world system security  

---

## <span style="color:#2b6cb0">Technologies Used</span>

- **Linux** (Ubuntu-based systems)  
- **UFW** (Uncomplicated Firewall)  
- **Bash**  
- **IPv4 & IPv6**  
- **ICMP / ping testing**  

---

## <span style="color:#2b6cb0">Objectives</span>

- Configure UFW to enforce secure network boundaries  
- Set and verify default inbound/outbound policies  
- Enable and evaluate firewall logging  
- Manage service-specific rules (HTTP, HTTPS, SSH)  
- Understand IPv4 vs. IPv6 rule creation  
- Troubleshoot connectivity using ICMP tools  

---

## <span style="color:#2b6cb0">Key Achievements</span>

- **Configured secure default firewall posture**  
  *Set “deny incoming” and “allow outgoing” baseline.*

- **Enabled and validated service-specific rules**  
  *Opened ports 22, 80, 443 without unnecessary duplicates.*

- **Managed duplicate rules efficiently**  
  *Demonstrated removal of redundant or conflicting entries.*

- **Enabled and reviewed UFW logging**  
  *Captured allow/deny activity to support troubleshooting.*

- **Differentiated IPv4 and IPv6 rule behavior**  
  *Ensured complete coverage across both protocols.*

- **Performed successful connectivity and rule validation tests**  
  *Verified enforcement using ICMP ping and UFW status reports.*

---

## <span style="color:#2b6cb0">Skills Demonstrated</span>

- **Linux System Administration**  
- **Firewall Configuration & Hardening**  
- **Traffic Filtering (IPv4 & IPv6)**  
- **Rule Creation, Deletion, and Management**  
- **Logging and Visibility Enhancements**  
- **Troubleshooting Network Connectivity**  

---

## <span style="color:#2b6cb0">Firewall Configuration Walkthrough</span>

---

### <span style="color:#2b6cb0">Step 1: Verify Firewall Status</span>

```bash
sudo ufw status
```

**Example Output:**
```
Status: active
To                         Action      From
22/tcp                     ALLOW       Anywhere
Anywhere                   DENY        192.168.1.100
22/tcp (v6)                ALLOW       Anywhere (v6)
```

---

### <span style="color:#2b6cb0">Step 2: Configure Default Policies</span>

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

Creates a **secure baseline**: inbound traffic blocked unless explicitly allowed.

---

### <span style="color:#2b6cb0">Step 3: Allow Specific Services</span>

```bash
sudo ufw allow http
sudo ufw allow https
sudo ufw allow 80
sudo ufw allow 443
```

> **Note:** Running both `allow http` and `allow 80` creates duplicate rules.  
> Use deletion to clean up:

```bash
sudo ufw delete allow 80
```

---

### <span style="color:#2b6cb0">Step 4: Verify Connectivity</span>

```bash
ping -c 4 8.8.8.8
```

Confirms outbound traffic is allowed.

---

### <span style="color:#2b6cb0">Step 5: Enable Firewall Logging</span>

```bash
sudo ufw logging on
```

Logs stored at:

```
/var/log/ufw.log
```

---

### <span style="color:#2b6cb0">Step 6: Verify Final Configuration</span>

```bash
sudo ufw status verbose
```

**Checks:**

- Default inbound/outbound policies  
- IPv4 & IPv6 rules  
- Logging level  
- Any deny/allow rules in effect  

---

### <span style="color:#2b6cb0">Step 7: Manage Rules Dynamically</span>

```bash
sudo ufw allow <port/service>
sudo ufw deny <port/service>
sudo ufw delete allow <port/service>
```

Examples:

```bash
sudo ufw deny 23/tcp
sudo ufw delete allow http
```

---

## <span style="color:#2b6cb0">Key Takeaways</span>

- UFW provides a **simple yet powerful** firewall interface  
- Default deny/allow rules create a strong security baseline  
- Duplicate rules can occur (service vs port syntax) and should be managed intentionally  
- IPv4 and IPv6 rules are created separately and must be handled as such  
- Logging provides visibility into allow/deny decisions  
- Connectivity testing is essential for validating configuration changes  

---

## <span style="color:#2b6cb0">Recommendations for Future Enhancements</span>

- Implement **rate limiting** for SSH (e.g., `ufw limit ssh`)  
- Add **application profiles** under `/etc/ufw/applications.d/`  
- Explore **nftables** as next-level firewall configuration  
- Add monitoring using tools like **Fail2Ban**  
- Test UFW rule conflicts and ordering behavior  

---

