# 📌 Advanced QoS Priority Controller using SDN (POX + Mininet)

---

## 📖 Problem Statement

Design and implement a **Software Defined Networking (SDN) based QoS controller** that prioritizes different types of network traffic using OpenFlow rules.

The controller dynamically classifies traffic (HTTP, HTTPS, FTP, SMTP, ICMP) and assigns priority levels to optimize network performance.

---

## 🎯 Objectives

* Identify multiple traffic types (HTTP, HTTPS, FTP, SMTP, ICMP)
* Assign priority levels based on protocol importance
* Install OpenFlow rules dynamically
* Implement **idle timeout (soft timeout)** and **hard timeout**
* Measure latency and throughput impact

---

## 🧠 Concept Overview

Traditional networks treat all packets equally. Using SDN:

* Traffic is centrally controlled
* Flow rules are dynamically installed
* Critical traffic gets priority

### Priority Mapping

| Protocol | Port | Priority     |
| -------- | ---- | ------------ |
| ICMP     | -    | 40 (Highest) |
| HTTPS    | 443  | 30           |
| HTTP     | 80   | 20           |
| SMTP     | 25   | 15           |
| FTP      | 21   | 10           |
| Others   | -    | 5 (Lowest)   |

---

## 🏗️ Network Topology

```
h1 ---- s1 ---- h2
          |
         h3
```

* h1: Client
* h2: Server
* h3: Additional host
* s1: OpenFlow switch
* POX Controller: Controls traffic

---

## ⚙️ Technologies Used

* Mininet
* POX Controller
* OpenFlow Protocol
* Python
* Open vSwitch

---

## 🛠️ Installation Steps

```bash
sudo apt update
sudo apt upgrade -y
sudo apt install mininet openvswitch-switch git python3 -y
cd ~
git clone https://github.com/noxrepo/pox.git
```

---

## ▶️ Execution Steps

### 1. Start Controller

```bash
cd ~/pox
./pox.py qos_controller
```

### 2. Start Mininet

(Open new terminal)

```bash
sudo mn --topo single,3 --controller remote
```

---

## 🧪 Testing Scenarios

### ✅ ICMP (Highest Priority)

```bash
h1 ping h2
```

---

### 🌐 HTTP (Port 80)

```bash
h2 python3 -m http.server 80 &
h1 wget http://10.0.0.2
```

---

### 🔐 HTTPS (Port 443)

```bash
h2 python3 -m http.server 443 &
h1 wget http://10.0.0.2:443
```

---

### 📁 FTP (Port 21)

```bash
sudo apt install python3-pyftpdlib
h2 python3 -m pyftpdlib -p 21 &
h1 ftp 10.0.0.2
```

---

### 📧 SMTP (Port 25)

```bash
h2 python3 -m smtpd -c DebuggingServer -n localhost:25 &
```

---

## 📊 Performance Metrics

### Latency

```bash
h1 ping -c 5 h2
```

### Throughput

```bash
h1 iperf -c h2
```

---

## 🔍 Flow Table Verification

```bash
sudo ovs-ofctl dump-flows s1
```

### Expected Output

* Flow entries with different priorities
* Timeout values:

  * idle_timeout = 10
  * hard_timeout = 30

---

## 🧩 SDN Logic

* Controller listens for **PacketIn events**
* Extracts protocol using TCP port numbers
* Installs flow rules using **match-action**
* Assigns:

  * Priority
  * Idle timeout
  * Hard timeout

---

## ⏱️ Timeout Explanation

* **Idle Timeout (Soft Timeout)**
  Removes flow if inactive for a certain time

* **Hard Timeout**
  Removes flow after fixed duration regardless of activity

---

## 📸 Proof of Execution

Include:

* Mininet running screenshot
* Controller logs showing protocol detection
* Ping results (ICMP)
* HTTP/HTTPS/FTP/SMTP execution
* Flow table output

---

## ✅ Functional Features

* Multi-protocol traffic classification
* Dynamic flow rule installation
* Priority-based QoS
* Timeout-based flow control
* Performance evaluation

---

## 🎤 Viva Explanation

> “The controller classifies traffic based on TCP port numbers and assigns different priorities. Higher priority traffic like ICMP and HTTPS is processed faster. Flow rules include idle and hard timeouts to dynamically manage network behavior.”

---

## 📚 References

* POX Documentation
* Mininet Documentation
* OpenFlow Specification

---

## 👨‍💻 Author

Name: [AKKINENI AKHIL]
Project: Advanced QoS Priority Controller
Course: SDN / Computer Networks

---

## 🎯 Conclusion

This project demonstrates how SDN enables flexible and dynamic QoS management. By prioritizing traffic and applying timeouts, the network adapts efficiently to different workloads.

---
