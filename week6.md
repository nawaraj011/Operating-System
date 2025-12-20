
# Week 6 — Performance Evaluation & Analysis

**[← Week 5](week5.md)** | **Week 6** | **[Week 7 →](week7.md)**

---

## 📋 Overview

This week executes the planned performance tests and analyses system behaviour under **baseline**, **load**, and **optimised** conditions. Using the applications selected in **Week 3** and the monitoring scripts prepared in **Week 5**, metrics are collected and analysed to identify bottlenecks, quantify improvements, and evaluate **security–performance trade-offs**.

All tests were conducted remotely via **SSH** on a hardened system with a verified security baseline.

---

## 🎯 Objectives

- Execute performance tests for each selected application
- Capture metrics: CPU, RAM, Disk I/O, Network, Response Time
- Compare baseline vs load vs optimised states
- Produce tables and visualisations
- Identify bottlenecks and measure optimisation impact

---

## 📦 Deliverables

- CSV performance datasets (`data/`)
- Graphs and charts (`docs/assets/`)
- Testing evidence (command outputs & screenshots)
- Network performance analysis
- Optimisation comparisons (before / after)

---

## 🖥️ Test Environment

| Component           | Details                        |
| ------------------- | ------------------------------ |
| OS                  | Ubuntu Server                  |
| Access              | SSH only                       |
| Monitoring          | `scripts/monitor-server.sh`    |
| Baseline Validation | `scripts/security-baseline.sh` |

All tests were executed with a **verified security baseline**.

---

## 🔄 Testing Flow

### 1. Baseline (Idle) Capture

```bash
./scripts/monitor-server.sh user@server data/baseline.csv 10
````

* System left idle to establish reference metrics

📸 **Screenshot**

![Baseline idle metrics](imagesss/week1/week6/.png)

---

### 2. CPU Performance Test

```bash
ssh user@server "stress-ng --cpu 4 --timeout 120"
```

* CPU utilisation and scheduler behaviour monitored

---

### 3. Disk I/O Performance Test

```bash
ssh user@server "fio --name=randrw --rw=randrw --bs=4k --size=1G --iodepth=16 --numjobs=2 --time_based --runtime=120"
```

* Measures disk throughput, latency, and queue depth

---

### 4. Network Performance Test

**Server:**

```bash
iperf3 -s
```

**Client (Workstation):**

```bash
iperf3 -c <server-ip> -t 60
```

📸 **Screenshot**

![Network throughput](imagesss/week1/week6/network.png)

* TCP throughput and jitter measured

---

### 5. Server / Service Test (nginx)

```bash
curl -w "%{time_total}\n" -o /dev/null -s http://<server-ip>
```

* Response time under idle and concurrent requests captured

---

## ⚙️ Optimisation Scenarios

* **Memory:** `sudo sysctl vm.swappiness=10`
* **CPU:** CPU governor tuned (if supported)
* **Web server:** nginx workers & connections adjusted
* **Disk:** I/O scheduler selection

Each optimisation followed by **full re-test**.

---

## 📊 Data Capture & Organisation

CSV files stored in `data/`:

* `baseline.csv`
* `cpu-load.csv`
* `disk-io.csv`
* `network.csv`
* `nginx-load.csv`

### CSV Schema

| Column    | Description                   |
| --------- | ----------------------------- |
| timestamp | Sample timestamp              |
| test_name | Test identifier               |
| metric    | Metric name                   |
| value     | Measured value                |
| units     | Measurement units             |
| notes     | Context or optimisation state |

Raw logs stored in `data/logs/`.

📸 **Screenshot**

![CSV data files](imagesss/week1/week6/cvs dataflkies.png)

---

## 📈 Results & Visualisation

* **Line graphs:** baseline vs load vs optimised
* **Bar charts:** throughput & latency comparisons

---

## 🔍 Analysis & Findings

### Bottlenecks

| Workload | Observation                              |
| -------- | ---------------------------------------- |
| CPU      | Saturation at sustained 100%             |
| Disk     | Latency spikes at high queue depth       |
| Network  | Throughput limited by NIC & TCP window   |
| nginx    | Response time increases with concurrency |

### Optimisation Impact

| Test     | Metric            | Before | After | Improvement |
| -------- | ----------------- | ------ | ----- | ----------- |
| Memory   | Swap usage        | 220 MB | 40 MB | ~82% ↓      |
| Disk I/O | Avg latency       | 18 ms  | 12 ms | ~33% ↓      |
| nginx    | Avg response time | 120 ms | 85 ms | ~29% ↓      |

---

## 🛡️ Security vs Performance

* AppArmor overhead <2% CPU
* fail2ban: no measurable impact
* Automatic updates scheduled outside peak testing
* Security remained fully enabled during tests

---

## 💭 Reflection

* CPU saturation was the main bottleneck
* Disk latency improvements gave largest gains
* Optimisations effective when workload-specific
* Security controls minimally impacted performance

---

## ✅ Conclusion

Week 6 validated the **full performance testing lifecycle**:

* Planning → Secure configuration → Execution → Optimisation → Analysis
* Demonstrated high performance while maintaining strong security posture

---

**[← Week 5](week5.md)** | **Week 6** | **[Week 7 →](week7.md)**

