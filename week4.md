# Week 4: Initial Configuration & Security Implementation

> **Focus:** Implementing core security controls and hardening remote access  
> **Environment:** Remote administration via SSH only

## 📋 Overview

This week focuses on implementing core security controls planned in earlier phases. The primary goal is to harden remote access, restrict network exposure, and enforce least-privilege administration on the Ubuntu Server. All configuration and evidence collection are performed remotely via SSH, with no local console access, to reflect real-world server administration practices.

---

## 🎯 Objectives

- Configure SSH key-based authentication and disable password login
- Restrict SSH access via firewall rules to the workstation IP only
- Create a non-root administrative user with least privilege
- Document configuration changes with before/after evidence
- Demonstrate secure remote administration via SSH

## 📦 Deliverables

- **SSH configuration evidence:** `/etc/ssh/sshd_config` before/after diff and reload output
- **Firewall ruleset verification:** `ufw status numbered`
- **User and privilege setup evidence:** `adduser`, `usermod`, and `/etc/sudoers.d/<admin>`
- **Remote evidence:** screenshots of successful SSH sessions from workstation
- **Proof of remote administration:** commands executed via SSH only

---

## 🔐 SSH Key-Based Authentication & Hardening

### Key Configuration

**SSH host keys verification and generation:**
```bash
sudo ssh-keygen -A
```

**User public keys placement:**
```bash
mkdir -p ~/.ssh
chmod 700 ~/.ssh
nano ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
```

---

### SSH Daemon Hardening

**Edit SSH daemon configuration:**
```bash
sudoedit /etc/ssh/sshd_config
```

**Key security settings applied:**

| Setting | Value | Purpose |
|---------|-------|---------|
| `PermitRootLogin` | `no` | Disable direct root access |
| `PasswordAuthentication` | `no` | Enforce key-based authentication only |
| `PubkeyAuthentication` | `yes` | Enable public key authentication |
| `AllowUsers` | `<admin>` | Restrict SSH access to specific user |
| `X11Forwarding` | `no` | Disable X11 for security |

**Restart SSH service to apply changes:**
```bash
sudo systemctl restart sshd
sudo systemctl status sshd
```

---

### SSH Configuration Evidence

**Capture configuration changes:**
```bash
diff -u sshd_config.before sshd_config.after
```

**Evidence collected:**
- Before and after configuration comparison
- Screenshot showing successful SSH login using key-based authentication only
- Service status confirmation after restart

---

## 🔥 Firewall Configuration (UFW)

### Firewall Policy

**Default-deny posture implementation:**
```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

**Restrict SSH access to workstation IP only:**
```bash
sudo ufw allow from 192.168.56.1 to any port 22 proto tcp
```

**Enable and verify firewall:**
```bash
sudo ufw enable
sudo ufw status numbered
```

---

### Firewall Evidence

**Verification commands:**
```bash
sudo ufw status numbered
sudo ufw status verbose
```

**Confirmation:**
- `ufw status numbered` output captured
- SSH is the only permitted inbound service
- All other incoming traffic is blocked by default

---

## 👤 Non-Root Administrative User Setup

### User Creation

**Create dedicated administrative user:**
```bash
sudo adduser <admin>
```

**Grant sudo privileges:**
```bash
sudo usermod -aG sudo <admin>
```

---

### Sudo Configuration

**Configure least-privilege sudo access:**
```bash
sudo visudo -f /etc/sudoers.d/<admin>
```

**Key considerations:**

| Configuration | Decision | Rationale |
|---------------|----------|-----------|
| Passwordless sudo | Disabled unless justified | Maintains accountability |
| Root shell access | No blanket access | Limits privilege scope |
| Configuration validation | Using `visudo` | Prevents syntax errors |

---

## 🖥️ Remote Administration Evidence

**Verification commands executed from workstation SSH session:**
```bash
whoami
hostname
ip addr
```

**Screenshots confirm:**
- ✅ Login as non-root admin user
- ✅ Successful sudo elevation
- ✅ All administration performed remotely via SSH
- ✅ No local console access required

---

## 💭 Reflection (Week 4)

### Security Impact

| Improvement | Description |
|-------------|-------------|
| **SSH attack surface reduced** | Password authentication eliminated, only key-based access allowed |
| **Network access restricted** | Firewall rules limit SSH to single trusted IP |
| **Root login disabled** | Enforces accountability and least privilege principle |

---

### Challenges & Recovery

**Risk mitigation strategies:**

- **SSH lockout prevention:** Kept an active session during changes
- **Firewall testing:** Rules tested before enabling enforcement
- **Service verification:** SSH service reload verified before disconnecting

---

### Design Justification

| Decision | Justification |
|----------|---------------|
| **IP-based firewall restrictions** | Chosen over broader access to minimise exposure |
| **Key-based SSH authentication** | Selected for strong cryptographic security |
| **Non-root admin user** | Improves auditability and limits damage from compromise |

---

### Comparison to Week 1

| Metric | Week 1 (Baseline) | Week 4 (Hardened) |
|--------|-------------------|-------------------|
| **Open ports** | Multiple defaults | SSH-only |
| **Remote access** | Password-based | Key-based authentication |
| **Privilege escalation** | Direct root login possible | Controlled via sudo |
| **Network exposure** | Unrestricted | IP-restricted firewall rules |

---

## 📊 Security Configuration Summary

### Before Hardening
- Password authentication enabled
- Root login allowed
- No firewall configured
- Unrestricted SSH access

### After Hardening
- ✅ Key-based authentication only
- ✅ Root login disabled
- ✅ UFW firewall enabled with default-deny
- ✅ SSH restricted to workstation IP (192.168.56.1)
- ✅ Non-root administrative user configured
- ✅ Least-privilege sudo access

---

## ✅ Week 4 Summary

Successfully implemented core security controls:

- 🔐 **SSH hardened** with key-based authentication and restricted access
- 🔥 **Firewall configured** with default-deny policy and IP restrictions
- 👤 **Administrative user created** with least-privilege sudo access
- 📸 **Remote administration demonstrated** via SSH-only access
- 🛡️ **Attack surface minimized** through multiple security layers

---

## 📄 Next Steps

- [ ] Week 5: Additional security hardening
- [ ] Week 6: Service deployment and testing
- [ ] Week 7: Performance baseline measurements and Comprehensive security audit

---
