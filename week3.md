# Week 3: Application Selection for Performance Testing

> **Focus:** Selecting representative applications to evaluate OS performance  
> **Environment:** Headless Ubuntu Server managed via SSH

## 📋 Overview

This week focuses on selecting representative applications to evaluate operating system performance under different workload categories. Each application was chosen based on how it stresses specific OS resources, including CPU scheduling, memory management, disk I/O, and network throughput. All tools are installed and managed via SSH using command-line utilities only, ensuring a headless, lightweight, and production-representative environment.

Expected resource utilisation patterns are defined in advance to support meaningful comparison between baseline (idle) and active workload states in later weeks.

---

## 🎯 Objectives

- Select applications that stress different system resources
- Document installation commands using SSH only
- Define expected resource utilisation profiles per application
- Establish a monitoring strategy for each workload type

## 📦 Deliverables

- **Application Selection Matrix** covering CPU, RAM, disk I/O, network, and server workloads
- **Installation documentation** with exact packages and commands
- **Expected resource profiles** and monitoring plan

---

## 📊 Selected Workload Categories

The following workload types are evaluated:

- **CPU-intensive**
- **Memory (RAM)-intensive**
- **Disk / I/O-intensive**
- **Network-intensive**
- **Server / service-based workload**

---

## 🔧 Application Selection Matrix

| Workload Type | Application | Description | Justification |
|---------------|-------------|-------------|---------------|
| **CPU-intensive** | `stress-ng` | CPU stress testing tool | Generates controlled CPU load to evaluate scheduling, load handling, and saturation behaviour |
| **RAM-intensive** | `stress-ng` (vm workers) | Memory stress testing | Allocates and stresses RAM to analyse memory management, paging, and swap behaviour |
| **I/O-intensive** | `fio` | Flexible I/O tester | Simulates realistic disk read/write workloads to evaluate filesystem and disk performance |
| **Network-intensive** | `iperf3` | Network performance testing tool | Measures bandwidth, throughput, and latency over TCP/UDP connections |
| **Server workload** | `nginx` | Lightweight web server | Represents a real-world service handling concurrent client requests |

---

## 💻 Installation Documentation (via SSH)

### SSH Access Verification

Successful SSH connection from Ubuntu Desktop workstation to Ubuntu Server:

```bash
ssh user@192.168.56.103
```

**Figure 3.1:** Successful SSH connection demonstrating secure remote command-line administration. This confirms that the server is managed remotely without local GUI access.

---

### Installed Applications

All tools were installed using APT over SSH:

```bash
sudo apt update
sudo apt install -y stress-ng fio iperf3 nginx sysstat
```

**Figure 3.2:** Installation of performance testing applications on Ubuntu Server using SSH. These tools collectively represent CPU, memory, disk, network, and server workloads.

---

### Application Verification

Installed applications were verified using version checks:

```bash
stress-ng --version
fio --version
iperf3 --version
nginx -v
```

**Figure 3.3:** Version output confirming successful installation and readiness for testing.

---

## 📈 Monitoring Strategy

### Baseline Measurement

Before executing any workloads, baseline system utilisation is captured:

```bash
top -bn1
free -h
vmstat 1 5
iostat -xz 5
uptime
```

**Figure 3.4:** Baseline system resource usage (idle state). Baseline metrics provide a reference point for comparison during active testing.

---

### CPU Workload Observation

```bash
stress-ng --cpu 4 --timeout 60s
```

**Figure 3.5:** CPU utilisation during stress-ng execution, demonstrating processor saturation under controlled load.

---

### Server Application Evidence

```bash
systemctl status nginx
```

**Figure 3.6:** nginx service running successfully as a representative server-based workload.

---

## 📊 Expected Resource Profiles

The table below documents anticipated system behaviour for each application prior to testing:

| Application | CPU Usage | Memory Usage | Disk I/O | Network Usage | Notes |
|-------------|-----------|--------------|----------|---------------|-------|
| **stress-ng (CPU)** | Very High | Low | Minimal | None | Saturates CPU cores |
| **stress-ng (RAM)** | Moderate | Very High | Possible swap | None | Tests memory pressure |
| **fio** | Low–Moderate | Low | Very High | None | Disk read/write focus |
| **iperf3** | Moderate | Low | Minimal | Very High | Network throughput testing |
| **nginx** | Low–Moderate | Low–Moderate | Low | Moderate–High | Simulates server workload |

*Predictions are based on documentation, prior experience, and workload characteristics.*

---

## 🔍 Monitoring Tools and Metrics

### Monitoring Tools

| Tool | Purpose |
|------|---------|
| `top` / `htop` | CPU and memory usage |
| `free -h` | Memory statistics |
| `vmstat` | System load and memory behaviour |
| `iostat -xz 5` | Disk I/O performance |
| `iftop` / `ss -tulpn` | Network activity |
| `uptime` | Load averages |

### Measurement Approach

- Capture baseline measurements before workload execution
- Record metrics during application execution
- Use consistent sampling intervals to ensure fair comparison
- Store outputs for later analysis and visualisation

---

## 📸 Evidence Collected

- ✅ SSH terminal screenshots showing installation commands
- ✅ CLI outputs verifying installed applications
- ✅ Monitoring screenshots (idle vs active states)
- ✅ Service status outputs for nginx and iperf3

---

## 📷 Image Captions Reference

| Figure | Description |
|--------|-------------|
| **Figure W3-1** | stress-ng version output confirming installation |
| **Figure W3-2** | fio version output confirming installation |
| **Figure W3-3** | iperf3 version output confirming installation |
| **Figure W3-4** | nginx version output confirming installation |
| **Figure W3-5** | stress-ng CPU workload execution and output |
| **Figure W3-6** | stress-ng memory workload execution |
| **Figure W3-7** | fio disk I/O workload evidence |
| **Figure W3-8** | iperf3 server listening state |
| **Figure W3-9** | iperf3 client-side throughput test |
| **Figure W3-10** | Network monitoring during iperf3 testing |

---

## 💭 Reflection (Week 3)

This week emphasised understanding how different workload types stress specific operating system components. Selecting appropriate tools highlighted the importance of aligning workloads with measurable OS behaviours. The planning performed this week establishes a strong foundation for performance testing, analysis, and optimisation in subsequent phases.

### Key Takeaways

- Each workload category targets specific OS subsystems
- Command-line tools provide precise, scriptable testing
- Baseline measurements are essential for meaningful comparison
- SSH-based management ensures production-like environment

---

## 📄 Next Week Preview (Week 4)

- [ ] Implement SSH key-based authentication
- [ ] Configure firewall rules (UFW)
- [ ] Create non-root administrative user
- [ ] Begin secure remote administration

---

## ✅ Week 3 Summary

Successfully selected and installed performance testing applications:

- 🖥️ **5 applications** covering all major resource categories
- 📦 **Installed via SSH** using standard package management
- 📊 **Expected profiles defined** for each workload type
- 🔍 **Monitoring strategy established** for comprehensive testing

