# Phase 2: Security Planning & Baseline Verification

← **[Week 1](week1.md)** | **Week 2** | **[Week 3 →](week3.md)**

---

## 📋 Overview

Week 2 focuses on **security planning and baseline verification** before applying any hardening changes. The objective is to validate secure access, observe the system’s default state, and collect baseline evidence that will be used for comparison in later weeks.

All activities are performed remotely via **SSH**, maintaining a secure and headless server environment.

---

## 🎯 Objectives

- Verify secure SSH access
- Establish baseline system performance metrics
- Inspect active services and network exposure
- Validate user privilege and sudo configuration
- Prepare the system for controlled security hardening

---

## 📦 Deliverables

- SSH key-based access verification
- Baseline system performance evidence
- Active service and network inspection
- User and sudo privilege validation
- Screenshot-based documentation

---

## 1. SSH Key-Based Authentication

Key-based SSH authentication was generated and deployed to ensure secure, password-less access.

📸 **Screenshot**  
Filename: `ssh-keygen.png`

![SSH key generation](imagesss/week2/ssh-keygen.png)

**Figure W2-1:** SSH key pair generation on the workstation.

---

📸 **Screenshot**  
Filename: `ssh-copy-id.png`

![SSH key deployment](imagesss/week2/ssh-copy-id.png)

**Figure W2-2:** Public SSH key successfully copied to the server.

---

## 2. Network Configuration Verification

The server’s network configuration was reviewed to confirm correct IP addressing and interface setup.

📸 **Screenshot**  
Filename: `ipaddr.png`

![IP address configuration](imagesss/week2/ipaddr.png)

**Figure W2-3:** Network interface configuration and assigned IP addresses.

---

## 3. Active Services and Listening Ports

Listening services and open ports were inspected to identify potential exposure.

📸 **Screenshot**  
Filename: `SUDOSS-TULPN.png`

![Listening services](imagesss/week2/SUDOSS-TULPN.png)

**Figure W2-4:** Active listening ports and associated services.

---

## 4. Baseline System Performance Metrics

Baseline resource utilisation was captured before applying any workload or security changes.

### Memory Usage

📸 **Screenshot**  
Filename: `free-h.png`

![Memory usage](imagesss/week2/free-h.png)

**Figure W2-5:** Memory usage in idle state.

---

### Disk Usage

📸 **Screenshot**  
Filename: `df-h.png`

![Disk usage](imagesss/week2/df-h.png)

**Figure W2-6:** Disk space allocation and utilisation.

---

### Process Monitoring

📸 **Screenshot**  
Filename: `htop.png`

![Process monitoring](imagesss/week2/htop.png)

**Figure W2-7:** Active processes and CPU utilisation.

---

## 5. Service Management Verification

Service control functionality was verified using systemd.

📸 **Screenshot**  
Filename: `servicecontrol.png`

![Service control](imagesss/week2/servicecontrol.png)

**Figure W2-8:** System service status and control via systemctl.

---

## 6. User and Sudo Privilege Validation

User privilege configuration was reviewed to ensure proper sudo access without direct root login.

📸 **Screenshot**  
Filename: `usermanagementsudo.png`

![User and sudo management](imagesss/week2/usermanagementsudo.png)

**Figure W2-9:** User account configuration and sudo permissions.

---

## 📝 Baseline Observations

- SSH access secured using key-based authentication
- Minimal services exposed on the network
- System resources show low utilisation in idle state
- Disk and memory usage within expected limits
- Sudo privileges correctly assigned to non-root user

---

## ✅ Phase 2 Summary

* Secure SSH access established
* Baseline performance metrics collected
* Network and service exposure documented
* User privilege model verified
* System prepared for security hardening

---

## ➡️ Next Phase — Week 3

Week 3 will focus on **application selection and workload preparation** for structured performance testing.

← **[Week 1](week1.md)** | **Week 2** | **[Week 3 →](week3.md)**
