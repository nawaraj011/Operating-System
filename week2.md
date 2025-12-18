Good — now I **fully understand** your repo and what you want.

You want **Week 2 report content**,
✅ **NO tree changes**
✅ `.md` files in **root**
✅ images inside **`imagesss/week2/`**
✅ images **must show on GitHub**

Your tree (confirmed):

```
.
├── imagesss/
│   ├── week1/
│   ├── week2/
│   │   ├── SUDOSS-TULPN.png
│   │   ├── df-h.png
│   │   ├── free-h.png
│   │   ├── htop.png
│   │   ├── ipaddr.png
│   │   ├── servicecontrol.png
│   │   ├── ssh-copy-id.png
│   │   ├── ssh-keygen.png
│   │   └── usermanagementsudo.png
├── week2.md
```

So the **ONLY correct image path** is:

```
imagesss/week2/filename.png
```

---

# ✅ FINAL — WEEK 2 REPORT (`week2.md`)

Copy-paste **exactly this** 👇

---

````md
# Week 2: Security Planning & Testing Methodology

> **Focus:** Performance testing methodology and security baseline design  
> **Approach:** Plan before implementation using a defense-in-depth strategy

---

## 📋 Overview

This week focuses on designing a comprehensive performance testing methodology and a security baseline for a Linux server deployment. The objective is to define *what will be measured*, *how evidence will be collected*, and *how risks will be mitigated* before making system changes.

---

## 🎯 Objectives

- Design a remote performance testing methodology
- Define a security configuration checklist before implementation
- Develop a threat model with concrete risks and mitigations

---

## 📦 Deliverables

- Performance testing plan
- Security hardening checklist
- Threat model
- Planned evidence collection strategy

---

## 1. Performance Testing Plan

### Remote Monitoring Methodology

- Monitoring performed remotely via SSH
- Use native Linux command-line tools
- Collect metrics at fixed intervals
- Capture evidence via screenshots and logs

**Example:**
```bash
ssh user@server "vmstat 5 5"
````

---

### Planned Metrics

| Category  | Metrics                   |
| --------- | ------------------------- |
| CPU       | Utilization, load average |
| Memory    | Free/used RAM, swap       |
| Disk      | I/O latency, usage        |
| Network   | Ports, throughput         |
| Processes | Resource consumption      |

---

### Tools and Commands

```bash
top
htop
free -h
df -h
ip addr
ss -tulpn
systemctl status
```

---

## 2. Security Configuration Checklist

### SSH Hardening Plan

* Disable root login
* Disable password authentication
* Enable key-based authentication
* Restrict SSH users
* Configure idle timeout

---

### Firewall Strategy (UFW)

* Default deny incoming
* Allow SSH from trusted IP
* Allow required service ports only
* Enable logging

---

### User Privilege Management

* Non-root admin user
* Least-privilege sudo access
* Regular user audits

---

## 3. Threat Model

### Threat 1: Unauthorized SSH Access

**Mitigations**

* SSH keys only
* Firewall IP restriction
* fail2ban

### Threat 2: Privilege Escalation

**Mitigations**

* sudo restrictions
* MAC enforcement
* Regular updates

### Threat 3: Service Exploitation

**Mitigations**

* Minimal services
* Firewall allowlist
* Monitoring & logs

---

## 📸 Evidence: Planned & Captured Screenshots

### SSH Key Generation

![SSH key generation](imagesss/week2/ssh-keygen.png)

### SSH Key Deployment

![SSH copy id](imagesss/week2/ssh-copy-id.png)

### Active Listening Services

![ss -tulpn](imagesss/week2/SUDOSS-TULPN.png)

### Memory Usage

![free -h](imagesss/week2/free-h.png)

### Disk Usage

![df -h](imagesss/week2/df-h.png)

### Process Monitoring

![htop](imagesss/week2/htop.png)

### Network Configuration

![ip addr](imagesss/week2/ipaddr.png)

### Service Control

![systemctl](imagesss/week2/servicecontrol.png)

### User & Sudo Management

![sudo management](imagesss/week2/usermanagementsudo.png)

---

## ✅ Week 2 Summary

* Security strategy planned before implementation
* Performance metrics clearly defined
* Threat model established
* Evidence collection prepared
* System ready for controlled hardening

---

## 📄 Next Step

➡️ **Week 3: Initial Implementation & SSH Hardening**

```

---

## ✅ WHY THIS WILL SHOW IMAGES ON GITHUB

✔ Correct relative paths  
✔ `.md` in root  
✔ Images in `imagesss/week2/`  
✔ No code blocks around images  
✔ Case-sensitive filenames respected  

---

If you want, next I can:
- Fix **Week 3–Week 7** the same way
- Audit the repo like a **university submission**
- Add a **README gallery** that auto-links weeks

Just say **“Week 3”** 👍
```
