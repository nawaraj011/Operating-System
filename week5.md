# Week 5 — Advanced Security & Monitoring

## Overview

This week builds on the foundational security controls implemented in **Week 4** by enabling advanced host-based security mechanisms and introducing automated monitoring and baseline validation scripts. The focus is on enforcing **Mandatory Access Control (MAC)**, hardening against brute-force attacks, ensuring timely patching, and preparing structured data collection for performance analysis in **Week 6**.

All configuration, validation, and scripting are performed remotely via **SSH** to maintain a headless, production-like environment.

---

## Objectives

* Enable and enforce Mandatory Access Control (MAC)
* Configure automatic security updates
* Deploy and configure `fail2ban` for SSH protection
* Build a security baseline verification script (`security-baseline.sh`)
* Build a remote monitoring script (`monitor-server.sh`) for performance data collection

---

## Deliverables

* MAC enforcement evidence (status commands and policy reports)
* Automatic update configuration evidence and logs
* `fail2ban` configuration, status output, and sample ban evidence
* Fully commented scripts with demonstration output

---

## Mandatory Access Control (MAC)

### MAC Selection

**AppArmor** is used on Ubuntu Server due to its native integration and profile-based enforcement model.

### AppArmor Status Verification

Verification command:

```bash
sudo aa-status
```

**Evidence confirms:**

* AppArmor is enabled and running
* Loaded profiles are in *enforce* mode
* Service-specific profiles (e.g., `nginx`, where applicable) are active and verified

---

## Automatic Security Updates

### Configuration

Automatic security updates are enabled using `unattended-upgrades`:

```bash
sudo apt update
sudo apt install -y unattended-upgrades
```

Configuration verified in:

```text
/etc/apt/apt.conf.d/50unattended-upgrades
```

**Key settings:**

* Security updates enabled
* Non-security updates disabled

### Verification Evidence

* Configuration file snippet captured
* Log verification:

```bash
journalctl -u unattended-upgrades
```

Logs confirm that automatic updates are active and functioning correctly.

---

## fail2ban Configuration

### Installation and Setup

```bash
sudo apt install -y fail2ban
```

Local jail configuration:

```bash
sudo nano /etc/fail2ban/jail.local
```

Example SSH jail configuration:

```ini
[sshd]
enabled  = true
port     = ssh
maxretry = 5
bantime  = 1h
findtime = 10m
```

### fail2ban Evidence

Verification commands:

```bash
sudo fail2ban-client status
sudo fail2ban-client status sshd
```

**Evidence includes:**

* Active SSH jail
* Number of failed authentication attempts
* Sample banned IP entries (if triggered during testing)

---

## Security Baseline Script

**Path:** `scripts/security-baseline.sh`

This script validates the server’s security posture against defined baseline requirements.

### Checks Performed

* SSH configuration (root login and password authentication)
* Firewall status and active rules (UFW)
* MAC enforcement status (AppArmor)
* Automatic update service status
* `fail2ban` service and jail state
* User and sudoers auditing
* Optional kernel security parameters

The script outputs a clear, readable summary and provides an exit status suitable for compliance audits.

---

## Monitoring Script

**Path:** `scripts/monitor-server.sh`

This script collects system performance metrics remotely and appends results to CSV files for later analysis.

### Metrics Collected

* CPU usage
* Memory consumption
* Disk I/O statistics
* Network activity
* Load averages

### Design Features

* Timestamped output
* Configurable sampling intervals
* Minimal performance overhead

Collected data will be visualised and analysed in **Week 6**.

---

## Evidence Collection

* Screenshots of MAC status (`aa-status`)
* Automatic update configuration files and logs
* `fail2ban` jail configuration and status output
* Script execution output from SSH sessions
* Generated CSV monitoring files

---

## Reflection (Week 5)

### Exceptions and Adjustments

* Firewall and `fail2ban` rules were adjusted to allow trusted workstation IPs
* AppArmor service profiles were reviewed to avoid disrupting legitimate application behaviour

### Performance Impact

* AppArmor enforcement introduced minimal CPU and memory overhead
* Automatic updates were scheduled to minimise runtime disruption
* Monitoring scripts were designed for low sampling overhead

### Preparation for Week 6

* Define workload durations and sampling intervals
* Confirm data storage structure for collected metrics
* Validate scripts under both idle and load conditions prior to final testing

---

