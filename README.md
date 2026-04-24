# QOS_CONTROLLER
# 📌 Simple QoS Priority Controller using SDN (POX + Mininet)

## 📖 Problem Statement

The objective of this project is to implement a **Quality of Service (QoS) Priority Controller** using Software Defined Networking (SDN). The system prioritizes certain types of network traffic over others using OpenFlow rules.

---

## 🎯 Objectives

* Identify different traffic types (ICMP, TCP)
* Assign priority levels to traffic
* Install flow rules dynamically using SDN controller
* Measure performance impact (latency and throughput)

---

## 🧠 Concept Overview

In traditional networks, traffic handling is static. Using SDN, we can:

* Dynamically control traffic
* Assign priorities
* Improve performance for critical packets

In this project:

* **ICMP (ping)** → High Priority
* **TCP (iperf)** → Low Priority

---

## 🏗️ Network Topology

```
h1 ---- s1 ---- h2
```

* h1: Sender
* h2: Receiver
* s1: OpenFlow Switch
* POX Controller: Controls flow rules

---

## ⚙️ Technologies Used

* Mininet
* POX Controller
* OpenFlow Protocol
* Python
* Open vSwitch

---

## 🛠️ Installation Steps

### 1. Install Dependencies

```bash
sudo apt update
sudo apt upgrade -y
sudo apt install mininet openvswitch-switch git python3 -y
```

### 2. Download POX

```bash
cd ~
git clone https://github.com/noxrepo/pox.git
```

### 3. Create Controller File

```bash
cd ~/pox/pox
nano qos_controller.py
```

Paste the controller code and save.

---

## ▶️ Execution Steps

### Step 1: Run POX Controller

```bash
cd ~/pox
./pox.py qos_controller
```

### Step 2: Run Mininet

(Open new terminal)

```bash
sudo mn --topo single,2 --controller remote
```

---

## 🧪 Testing & Validation

### ✅ Test Case 1: High Priority Traffic (ICMP)

```bash
h1 ping h2
```

* Expected: Faster response (low latency)

---

### ✅ Test Case 2: Low Priority Traffic (TCP)

```bash
h2 iperf -s &
h1 iperf -c h2
```

* Expected: Lower priority handling

---

## 📊 Performance Metrics

### Latency Measurement

```bash
h1 ping -c 5 h2
```

### Throughput Measurement

```bash
h1 iperf -c h2
```

---

## 🔍 Flow Table Verification

```bash
sudo ovs-ofctl dump-flows s1
```

Expected:

* High priority rule for ICMP
* Low priority/default rule for other traffic

---

## 📸 Proof of Execution

Include the following screenshots:

* Mininet topology running
* Ping results
* iperf results
* Flow table output
* Controller logs

---

## 🧩 SDN Logic

* Controller listens for **PacketIn events**
* Identifies packet type
* Installs flow rules using **match-action**
* Assigns priority dynamically

---

## ✅ Functional Features

* Traffic prioritization
* Dynamic flow rule installation
* Performance analysis
* Controller-switch interaction

---

## 📚 References

* POX Controller Documentation
* Mininet Documentation
* OpenFlow Specification

---

## 🎤 Conclusion

This project demonstrates how SDN can be used to implement QoS by dynamically controlling network traffic. High-priority traffic (ICMP) is handled efficiently compared to low-priority traffic (TCP), showcasing the flexibility of SDN.

---

## 👨‍💻 Author

Name: [Your Name]
Project: Simple QoS Priority Controller
Course: Computer Networks / SDN Lab

---
