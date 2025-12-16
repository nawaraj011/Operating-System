# Phase 1: System Planning and Distribution Selection

> **Timeline:** Week 1  
> **Environment:** VirtualBox Lab on Mac Laptop

## 📋 Overview

This phase covers the planning and setup of a VirtualBox lab environment using a laptop as the host machine. The environment consists of one Ubuntu Server and one Ubuntu Desktop Workstation configured with appropriate network modes for secure internal communication and internet access.

---

## 🖥️ System Configuration

### Ubuntu Server 22.04 LTS
- **Network Mode:** Host-Only
- **IP Address:** `192.168.56.103/24`
- **Purpose:** Isolated server environment

### Ubuntu Desktop 24.04 LTS
- **Network Mode:** NAT + Host-Only
- **IP Address (Host-Only):** `192.168.56.102/24`
- **Purpose:** Client workstation and control system

### Host Environment
- **Physical Host:** Mac Laptop
- **Virtualization Platform:** Oracle VirtualBox

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────┐
│                     Mac Laptop (Host)                    │
│                                                           │
│  ┌───────────────────────────────────────────────────┐  │
│  │            VirtualBox Environment                  │  │
│  │                                                     │  │
│  │  ┌─────────────────┐      ┌──────────────────┐   │  │
│  │  │ Ubuntu Server   │      │ Ubuntu Desktop   │   │  │
│  │  │   22.04 LTS     │◄────►│    24.04 LTS     │   │  │
│  │  │                 │      │                  │   │  │
│  │  │ Host-Only Only  │      │  NAT + Host-Only │   │  │
│  │  │ 192.168.56.103  │      │  192.168.56.102  │   │  │
│  │  └─────────────────┘      └──────────────────┘   │  │
│  │         │                          │              │  │
│  │         │                          │              │  │
│  │         └──────────┬───────────────┘              │  │
│  │                    │                              │  │
│  │         Host-Only Network (192.168.56.0/24)      │  │
│  │                                                     │  │
│  └───────────────────────────────────────────────────┘  │
│                           │                              │
└───────────────────────────┼──────────────────────────────┘
                            │
                      Internet (NAT)
```

### Network Design Features

- ✅ **Secure private communication** between server and workstation
- ✅ **Internet access** only from the workstation
- ✅ **Server isolation** from the internet for enhanced security
- ✅ **Static IP addressing** for predictable connections

---

## 📊 Distribution Selection Analysis

### Ubuntu Server 22.04 LTS ✔️ **Selected**

#### Pros
- ✅ Easy to use and beginner-friendly
- ✅ Huge repository of up-to-date software packages
- ✅ Large, active community with extensive documentation
- ✅ Excellent compatibility with VirtualBox and cloud platforms
- ✅ Frequent security updates with 5-year LTS support cycle

#### Cons
- ⚠️ Slightly less stable than Debian for ultra-long-term production use
- ⚠️ Uses more system resources than ultra-light distributions
- ⚠️ Some enterprise features require Ubuntu Pro subscription

---

### Alternative Distributions Considered

<details>
<summary><strong>Debian</strong></summary>

#### Pros
- Extremely stable and reliable
- Excellent long-term performance
- Strong security due to strict package testing
- Very lightweight, suitable for low-spec systems

#### Cons
- Packages are often outdated
- Manual configuration required
- Documentation can be very technical for beginners
- Less common in cloud environments compared to Ubuntu

</details>

<details>
<summary><strong>Red Hat Enterprise Linux (RHEL)</strong></summary>

#### Pros
- Enterprise-grade stability and performance
- Very strong security features
- Professionally supported
- Suitable for corporate data centers

#### Cons
- Requires paid subscription for full features
- Difficult for beginners and students
- Limited free repositories
- Slower software updates

</details>

---

## 🎯 Selection Justification

**Ubuntu Server** was selected as the most appropriate solution for this deployment because it offers the **best balance** between:

- 🎓 Ease of use for learning environments
- 📦 Modern software availability
- 🛡️ Long-term support
- 👥 Strong community backing
- 🔧 Full compatibility with VirtualBox

**Debian** is more stable but less beginner-friendly with older packages. **RHEL** is enterprise-focused but requires a paid subscription. Therefore, **Ubuntu Server is the most effective choice** for a learning and laboratory-based environment.

---

## 💻 Workstation Configuration

### Ubuntu Desktop 24.04 LTS

**VirtualBox Network Adapters:**
- **Adapter 1:** NAT
- **Adapter 2:** Host-Only (Static IP: `192.168.56.102/24`)

### Workstation Role

The Ubuntu Workstation was installed as a **client and control system** to:

- 🔐 Access the Ubuntu Server
- 🧪 Test client/server communication
- ⚙️ Perform administrative tasks
- 📥 Download and update packages from the internet
- 🎛️ Act as the control terminal for all server services

---

## 🌐 Network Configuration Details

### NAT Adapter – Internet Access

NAT allows the workstation to access the internet through the host machine.

**Required for:**
- System package updates and downloads
- Installing tools (OpenSSH client, curl, browsers)
- Accessing online documentation and resources

**Advantages:**
- ✅ Plug-and-play configuration
- ✅ No exposure of the VM to the public network
- ✅ Secure outbound-only internet access

### Host-Only Adapter – Internal Network

The Host-Only adapter provides a **private LAN** between:
- Host machine
- Ubuntu Server
- Ubuntu Workstation

**Enables:**
- 🔒 Direct SSH access to the server
- 🧪 Secure internal testing
- 🛡️ No exposure to the public internet

**Advantages:**
- ✅ Static IP addressing
- ✅ Predictable SSH connections
- ✅ Secure isolated network

---

## 📝 Network Configuration Summary

### Ubuntu Server

| Setting | Value |
|---------|-------|
| **VirtualBox Adapter** | Host-Only Adapter (vboxnet0) |
| **IP Address** | `192.168.56.103/24` |
| **Subnet Mask** | `255.255.255.0` |
| **Gateway** | None |
| **Internet Access** | None (Isolated by design) |

### Ubuntu Workstation

| Setting | Value |
|---------|-------|
| **Adapter 1** | NAT (DHCP for internet) |
| **Adapter 2** | Host-Only |
| **Host-Only IP** | `192.168.56.102/24` |
| **Subnet Mask** | `255.255.255.0` |
| **Gateway** | `192.168.56.1` |

---

## 🔧 System Specifications

### Commands Used
```bash
uname -a
free -h
df -h
ip addr
lsb_release -a
```

### System Information

| Component | Specification |
|-----------|---------------|
| **Kernel Version** | `6.14.0-27-generic` |
| **Architecture** | `x86_64` (64-bit) |
| **Operating System** | GNU/Linux |
| **Build** | Ubuntu SMP, PREEMPT_DYNAMIC |

### Memory Information

| Metric | Value |
|--------|-------|
| **Total RAM** | 3.8 GiB |
| **Used RAM** | 1.0 GiB |
| **Available RAM** | 2.8 GiB |
| **Swap** | 0 B |

### Disk Space

| Metric | Value |
|--------|-------|
| **Primary Disk Size** | 25 GB |
| **Used** | 5.1 GB |
| **Available** | 19 GB |
| **Root Filesystem** | `/dev/sda2` |

### Network Interfaces

| Interface | Network Type | IP Address | Purpose |
|-----------|--------------|------------|---------|
| `lo` | Loopback | `127.0.0.1` | Local processes |
| `enp0s3` | NAT | `10.0.2.15/24` | Internet access |
| `enp0s8` | Host-Only | `192.168.56.102/24` | Server communication |

### Distribution Information

| Property | Value |
|----------|-------|
| **Distribution** | Ubuntu |
| **Version** | 24.04.3 LTS |
| **Codename** | Noble |
| **Support** | Long-Term Support (LTS) |

---

## ✅ Phase 1 Summary

In Phase 1, I successfully planned and deployed a secure VirtualBox lab environment consisting of:

- 🖥️ **One isolated Ubuntu Server** using Host-Only networking
- 💻 **One Ubuntu Workstation** using NAT + Host-Only networking

### Key Achievements

✅ **Strong security** through server isolation  
✅ **Reliable internal communication** via Host-Only network  
✅ **Safe and controlled internet access** through the workstation only  
✅ **Production-ready lab environment** for further phases

---

## 📚 Next Steps

- [ ] Phase 2: Service Configuration
- [ ] Phase 3: Security Hardening
- [ ] Phase 4: Testing and Validation


---

