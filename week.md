# Week 2: Security Planning & Testing Methodology

> **Focus:** Performance testing methodology and security baseline design  
> **Approach:** Plan before implementation using defense-in-depth strategy

## 📋 Overview

This week focuses on designing a comprehensive performance testing methodology and a security baseline for a Linux server deployment. The goal is to plan before implementation—defining what will be measured, how evidence will be collected, and how security risks will be mitigated using a defence-in-depth approach.

---

## 🎯 Objectives

- Draft a performance testing approach for remote monitoring
- Build a security configuration checklist before touching the server
- Produce a threat model with at least three concrete threats and mitigations

## 📦 Deliverables

- **Performance testing plan:** metrics, tools, sampling intervals, automation strategy
- **Security checklist:** SSH hardening, firewall defaults, MAC (SELinux/AppArmor), updates, privilege management
- **Threat model:** threat actors, attack surfaces, mitigations

---

## 1. Performance Testing Plan

### Remote Monitoring Methodology

**Approach:**
- All performance monitoring will be conducted remotely via SSH from the workstation
- Data collection will rely on standard Linux command-line utilities
- Metrics will be captured at regular intervals to establish baseline and load/stress conditions
- Evidence will include terminal output, logs, and screenshots

**Remote Execution Example:**
```bash
ssh user@server "vmstat 5 5"
```

### Planned Metrics

| Category | Metrics Tracked |
|----------|----------------|
| **CPU** | Utilization, load average |
| **Memory** | Free/used RAM, swap activity |
| **Disk I/O** | Throughput, latency, utilization |
| **Network** | Throughput, listening ports, active connections |
| **Processes** | Responsiveness and resource consumption |

---

### Tools and Commands

**CPU Monitoring:**
```bash
top -bn1 | grep "Cpu(s)"
mpstat 1 5
```

**Memory Usage:**
```bash
free -h
vmstat 1 5
```

**Disk I/O:**
```bash
iostat -x 1 5
df -h
```

**Network Monitoring:**
```bash
ss -tulpn
iftop -t -s 5
nethogs -t
```

**System & Services:**
```bash
uname -a
systemctl status ssh
journalctl -xe
```

---

### Testing Approach

**Baseline Testing:**
- Capture metrics during idle state
- Record measurements over 5-minute intervals
- Establish normal operating parameters for CPU, memory, disk, and network usage

**Load Testing:**
- Apply controlled workloads using selected applications
- Monitor system behavior during peak usage
- Compare results against baseline metrics

**Data Collection Strategy:**
- Automated monitoring script (`monitor-server.sh`)
- Output logged in CSV format for analysis
- Screenshots captured with visible shell prompts for documentation

---

### Planned Command-Line Evidence

- System Information: `uname -a`
- Disk Performance: `iostat`
- Process & Directory Verification: `ls`, `top`
- Server Status: running services via `systemctl`
- SSH Configuration: `sshd_config`, service status
- Firewall Status: `ufw status`
- Memory Statistics: `vmstat`
- User Verification: `grep` on `/etc/passwd` and `/etc/group`

---

## 2. Security Configuration Checklist

### SSH Hardening

- Disable root login (`PermitRootLogin no`)
- Disable password authentication (`PasswordAuthentication no`)
- Enable key-based authentication only
- Restrict access to specific users (`AllowUsers <admin-user>`)
- Configure idle timeout (`ClientAliveInterval`, `ClientAliveCountMax`)
- Disable X11 forwarding if not required
- Optional: change default SSH port (with documented trade-offs)

---

### Firewall Configuration (UFW)

**Configuration Steps:**
```bash
# Install and enable UFW
sudo apt install ufw
sudo ufw enable

# Default deny all incoming traffic
sudo ufw default deny incoming

# Allow SSH from workstation IP only
sudo ufw allow from 192.168.56.1 to any port 22 proto tcp

# Allow only required service ports (document justification)
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp

# Enable logging for dropped packets
sudo ufw logging on

# Test firewall rules
sudo ufw status verbose
```

**Checklist:**
- Install and enable UFW
- Default deny all incoming traffic
- Allow SSH from workstation IP only
- Allow only required service ports (document justification)
- Enable logging for dropped packets
- Test firewall rules before disconnecting

---

### Mandatory Access Control (MAC)

| Distribution | MAC System | Reason |
|--------------|------------|--------|
| Ubuntu | **AppArmor** | Easier profile management, default integration |
| RHEL/Fedora/Rocky | **SELinux** | More powerful but complex |

**Implementation:**
- Use AppArmor (Ubuntu) or SELinux (RHEL/Fedora/Rocky)
- Enable and enforce MAC system
- Create or modify profiles for critical services
- Test application functionality under enforced policies
- Document all policy decisions

---

### Automatic Updates

```bash
# Install unattended-upgrades
sudo apt install unattended-upgrades

# Configure automatic security updates
sudo dpkg-reconfigure -plow unattended-upgrades
```

**Configuration:**
- Install and configure `unattended-upgrades`
- Enable automatic security updates only
- Schedule daily update checks
- Configure notifications (if applicable)
- Verify update functionality

---

### User Privilege Management

- Create a non-root administrative user
- Configure sudo with least-privilege principle
- Disable passwordless sudo unless justified
- Enforce strong password policies (for sudo)
- Remove unnecessary users and groups
- Review group memberships regularly

---

### Network Security Enhancements

- Disable IPv6 if not required
- Deploy fail2ban (planned jails: sshd, optional nginx)
- Disable unused network services
- Configure NTP for time synchronization
- Validate exposure using nmap

---

## 3. Threat Model

### Threat 1: Unauthorized SSH Access

**Risk Level:** High  
**Priority:** Phase 4

**Description:**  
Attackers attempt SSH brute-force attacks or exploit compromised credentials.

**Mitigations:**
- Key-based authentication only
- Disable root and password login
- Restrict SSH access by IP using firewall rules
- Deploy fail2ban for SSH
- Strong passphrase-protected SSH keys
- Monitor `/var/log/auth.log`

---

### Threat 2: Privilege Escalation

**Risk Level:** Medium–High  
**Priority:** Phase 5

**Description:**  
A compromised user account attempts to gain root access.

**Mitigations:**
- Enforce AppArmor/SELinux policies
- Least-privilege sudo configuration
- Automatic security updates
- Regular audits with Lynis
- Disable unnecessary SUID/SGID binaries
- Monitor sudo logs

---

### Threat 3: Service Exploitation

**Risk Level:** Medium  
**Priority:** Phases 4–7

**Description:**  
Vulnerabilities in exposed services are exploited remotely.

**Mitigations:**
- Minimize attack surface (essential services only)
- Firewall allowlist rules
- MAC confinement of services
- Regular vulnerability scanning (nmap, Lynis)
- Centralized log monitoring
- Maintain documented service inventory

---

## 💭 Reflection

### Key Decisions

| Decision | Justification |
|----------|---------------|
| **MAC Choice: AppArmor** | Selected for Ubuntu due to easier profile management and default integration |
| **Firewall Strategy: Strict allowlist** | Minimize exposed services and maintain tight control |
| **Security vs Usability** | Balanced by restricting access while maintaining remote manageability |

### Anticipated Challenges

- Secure SSH key storage and rotation
- Performance overhead of monitoring and MAC enforcement
- Complexity of custom AppArmor/SELinux policies
- Managing evidence collection consistently

### Learning Objectives

- Security planning and threat modeling
- Defense-in-depth strategy design
- Performance testing methodology
- Evaluating security vs performance trade-offs

---

## 📝 Notes & Evidence Plan

**Installation Requirements:**
```bash
# Install required tools if missing
sudo apt install sysstat iftop nethogs
```

**Data Organization:**
- Store logs and CSV output in `data/`
- Capture screenshots with timestamps and visible prompts
- Confirm commands for live demo in final video

---

## 📚 References

**Ubuntu Documentation — SSH & Server Security Guidance**  
Official server security best practices and SSH configuration guides  
https://documentation.ubuntu.com/server/how-to/security/openssh-server/

**Ubuntu Server Security Concepts & Best Practices**  
Overview of security strategies including authentication and system hardening  
https://ubuntu.com/server/docs/explanation/security/

**Ubuntu Wiki — Uncomplicated Firewall (UFW)**  
Official Ubuntu Wiki page about UFW configuration  
https://wiki.ubuntu.com/UncomplicatedFirewall

**Ubuntu Server Firewall Documentation**  
Official documentation on firewall basics and UFW usage  
https://documentation.ubuntu.com/server/how-to/security/firewalls/

---

## ✅ Week 2 Summary

Successfully planned a comprehensive security and testing strategy including:

- 📊 **Remote performance monitoring methodology** with defined metrics and tools
- 🔒 **Security configuration checklist** covering SSH, firewall, MAC, updates, and privileges
- ⚠️ **Threat model** with three identified threats and concrete mitigations
- 🛡️ **Defense-in-depth approach** for layered security protection

---

## 📄 Next Steps

- [ ] Phase 3: Begin Implementation
- [ ] Phase 4: SSH Hardening
- [ ] Phase 5: Privilege Management
- [ ] Phase 6: Service Deployment
- [ ] Phase 7: Final Testing

---
