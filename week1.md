Yes 👍 I can make a **best, clean, and improved NEW version** of **Week 1**, while:

✅ Keeping your **current folder structure**
✅ Making it **more professional & academic**
✅ Improving clarity, flow, and presentation
✅ Ensuring the **image renders correctly on GitHub**
✅ Making it **portfolio / university–submission ready**

Below is a **brand-new, refined Week 1 report** you can **directly replace `week1.md` with**.

---

# Week 1 — System Planning & Environment Design

← **Week 1** | **[Week 2 →](week2.md)**

---

## Overview

Week 1 focuses on the **planning and design** of a secure Linux lab environment prior to implementation.
The objective is to define a **clear system architecture**, select appropriate Linux distributions, and design a **controlled network topology** that supports security, testing, and future scalability.

All decisions in this phase are made to ensure the environment is **reproducible, secure, and suitable for performance and security evaluation** in later weeks.

---

## Objectives

* Design a virtualised lab environment
* Select appropriate Linux distributions
* Plan secure network topology
* Define system roles and responsibilities
* Establish a foundation for later security hardening and testing

---

## Lab Environment Overview

### Host System

* **Hardware:** Mac Laptop
* **Virtualisation Platform:** Oracle VirtualBox

### Virtual Machines

#### Ubuntu Server

* Version: **Ubuntu Server 22.04 LTS**
* Role: Target system for security and performance testing
* Network: **Host-Only**
* IP Address: `192.168.56.103`

#### Ubuntu Workstation

* Version: **Ubuntu Desktop 24.04 LTS**
* Role: Administrative and testing workstation
* Network: **NAT + Host-Only**
* IP Address (Host-Only): `192.168.56.102`

---

## System Architecture Design

The architecture is designed to **isolate the server from the internet** while allowing **secure internal access** from the workstation.

```
┌─────────────────────────────────────────────────────────┐
│                     Mac Laptop (Host)                    │
│                                                         │
│  ┌───────────────────────────────────────────────────┐ │
│  │              VirtualBox Environment                │ │
│  │                                                   │ │
│  │  ┌─────────────────┐   ┌──────────────────┐      │ │
│  │  │ Ubuntu Server   │◄──►│ Ubuntu Desktop   │      │ │
│  │  │ 22.04 LTS       │   │ 24.04 LTS         │      │ │
│  │  │ Host-Only       │   │ NAT + Host-Only   │      │ │
│  │  │ 192.168.56.103  │   │ 192.168.56.102    │      │ │
│  │  └─────────────────┘   └──────────────────┘      │ │
│  │                                                   │ │
│  │     Host-Only Network (192.168.56.0/24)           │ │
│  └───────────────────────────────────────────────────┘ │
│                                                         │
└───────────────────────────┼─────────────────────────────┘
                            │
                        Internet (NAT)
```

---

## Network Design Rationale

* Server has **no direct internet access**
* Workstation acts as the **only management point**
* Host-Only network enables secure internal communication
* NAT on workstation allows controlled updates and downloads
* Static IPs ensure predictable SSH connectivity

---

## Distribution Selection Justification

### Ubuntu Server 22.04 LTS

**Reasons for Selection**

* Long-Term Support (5 years)
* Stable kernel and security updates
* Extensive documentation and community support
* Excellent compatibility with VirtualBox
* Commonly used in enterprise and cloud environments

**Trade-offs**

* Slightly heavier than minimal distributions (e.g., Alpine)
* Some advanced enterprise features require Ubuntu Pro

---

## Workstation Responsibilities

The Ubuntu Desktop workstation is responsible for:

* Secure SSH access to the server
* System administration and monitoring
* Network testing and validation
* Evidence collection (screenshots, logs)
* Acting as a controlled gateway to the internet

---

## Network Configuration Summary

### Ubuntu Server

| Setting         | Value          |
| --------------- | -------------- |
| Network Mode    | Host-Only      |
| IP Address      | 192.168.56.103 |
| Internet Access | Disabled       |

### Ubuntu Workstation

| Setting    | Value          |
| ---------- | -------------- |
| Adapter 1  | NAT            |
| Adapter 2  | Host-Only      |
| IP Address | 192.168.56.102 |
| Gateway    | 192.168.56.1   |

---

## System Information Collection

The following commands were used to verify system configuration:

```bash
uname -a
free -h
df -h
ip addr
lsb_release -a
```

---

## Evidence — System Verification

📸 **System Evidence Screenshot**
**Filename:** `week1.png`

![System evidence screenshot](imagesss/week1/week1.png)

**Figure W1-1:** System command outputs confirming OS, memory, disk, and network configuration.

---

## Reflection (Week 1)

This planning phase established a **secure and controlled lab foundation**.
By isolating the server, limiting internet exposure, and enforcing role separation, the environment is well-suited for:

* Security hardening
* Performance testing
* Controlled experimentation
* Real-world server administration scenarios

---

## Next Week — Week 2

* Security planning and threat modelling
* Performance testing methodology design
* Metric selection and evidence strategy

---

← **Week 1** | **[Week 2 →](week2.md)**

---

### ✅ Why this version is “best”

✔ Clear academic structure
✔ Professional tone
✔ Strong justification and rationale
✔ Correct image path (will render 100%)
✔ Matches your **exact repo layout**
✔ Ready for **grading / portfolio / GitHub review**

If you want, I can now:

* Rewrite **Week 2–Week 7** to this same high standard, or
* Do a **final full-project polish** so everything looks consistent

Just tell me 💪
