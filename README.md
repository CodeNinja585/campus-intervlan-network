# 🧠 Campus Inter-VLAN Network Design (Cisco Packet Tracer)

> A complete simulation of an enterprise-level campus LAN with VLANs, inter-VLAN routing, DHCP, DNS, FTP/HTTP services, spanning tree protocol, and ACLs — designed in Cisco Packet Tracer.

---

## 🎯 Objectives

- Segment users into different VLANs (Sales & HR)
- Enable inter-VLAN communication using subinterfaces
- Prevent loops with STP
- Automatically assign IPs via DHCP
- Implement ACLs for HTTP access control
- Simulate DNS, FTP, and HTTP services

---

## 🧰 Tools & Devices

- **Cisco Packet Tracer**
- 2x L2 Switches (Switch0 & Switch1)
- 1x Router (with subinterfaces)
- 1x Server (DHCP, DNS, HTTP, FTP)
- Multiple PCs

---

## 🧱 Network Topology

📌 Topology screenshot:  
![Topology](./topology/Network_Topology.png)

| Device       | Interface      | Connected To    | VLAN / Purpose     |
|--------------|----------------|------------------|---------------------|
| Switch1      | Fa0/23         | Switch0 (Trunk) | VLAN 10, 20         |
| Switch1      | Fa0/24         | Router (Trunk)  | VLAN 10, 20         |
| Switch1      | Fa0/5          | Server          | VLAN 10             |
| Switch0      | Fa0/22         | Router (Trunk)  | VLAN 10, 20         |
| PCs          | Fa0/1–Fa0/4    | Switch1/0       | VLAN 10 / VLAN 20   |

---

## 🗺️ Topology Overview

| Device   | Interface  | Connected To | Interface  |
|----------|------------|--------------|------------|
| Switch1  | Fa0/23     | Switch0      | Fa0/22     |
| Switch1  | Fa0/24     | Router       | Gi0/0      |
| Server   | Fa0/5      | Switch1      | VLAN 10    |
| PCs      | Fa0/1–4    | Both Switches| VLAN 10/20 |

> 📌 See `/topology/` folder for diagram screenshots

---

## 🔧 Key Configurations

 All config files are available in [`/configs`](./configs).

### 🔸 VLAN & Trunk Config
```bash
Switch(config)# vlan 10
Switch(config-vlan)# name SALES
Switch(config)# vlan 20
Switch(config-vlan)# name HR
Switch(config)# interface fa0/23
Switch(config-if)# switchport mode trunk
```

###🔸 Router-on-a-Stick
```bash
Router(config)# interface GigabitEthernet0/0.10
Router(config-subif)# encapsulation dot1Q 10
Router(config-subif)# ip address 192.168.10.1 255.255.255.0

Router(config)# interface GigabitEthernet0/0.20
Router(config-subif)# encapsulation dot1Q 20
Router(config-subif)# ip address 192.168.20.1 255.255.255.0
```
###🔸DHCP Relay
```bash
Router(config)# interface GigabitEthernet0/0.10
Router(config-if)# ip helper-address 192.168.10.5

Router(config)# interface GigabitEthernet0/0.20
Router(config-if)# ip helper-address 192.168.20.5
```
---
### 📸 Screenshots
Browse all in /screenshots:

- show vlan brief
- show interfaces trunk
- DHCP service config
- DNS + HTTP/FTP service panels
- PC terminal ping tests
- ACL verification
---

### 🧪 Testing Results
✅ PCs in VLAN 10 and 20 successfully received IPs
✅ Inter-VLAN communication worked
✅ FTP and HTTP services accessible
✅ ACLs restricted unauthorized access as expected
✅ DNS resolutions successful
---

## 🔐 Services Configured on Server

- **DHCP:** Address pools for both VLANs
- **DNS:** Internal name resolution
- **HTTP/FTP:** File server for internal access

---

## ⚠️ Challenges & Fixes

### 🔴  DHCP Not Working on Switch1
- Issue: DHCP leases only issued to PCs on Switch0.
- **Cause:** Server wasn't trunked through correctly; VLANs weren’t forwarding on Switch1
- **Fix:** Ensured trunk ports carried VLAN 10/20 and configured ip helper-address on router subinterfaces.


### 🔴 HTTP Access Blocked
- **Issue:** VLAN 20 PCs couldn’t reach web service.
- **Cause:** ACL logic error + typo in IP range (192.169.20.0)
- **Fix:** Corrected ACL ordering and IP subnet
---

## 🧠 What I Learned
- Router-on-a-Stick configuration
- DHCP relay via ip helper-address
- ACL troubleshooting and security design
- Service simulation: DNS, FTP, HTTP in Packet Tracer
- Broadcast domains and trunk propagation

---

## 📘 Key Takeaways

- Practical use of **802.1Q trunking**
- Hands-on experience with **Router-on-a-Stick**
- Understanding of **broadcast domains** & DHCP relay
- Real-world **ACL troubleshooting**
- Applying **STP** to prevent loops

---

## 🔗 Further Reading

- [Part 1 on Medium](#) — VLANs, Routing, STP
- [Part 2 on Medium](#) — DHCP, DNS, ACLs, Services

---

## 🧠 Author

**Donald Likke**  
🔗 [LinkedIn](https://www.linkedin.com/in/donald-okputu-b7b431290/)
📁 [Portfolio](https://github.com/CodeNinja585)

---

📌 *This project was developed as part of my self-study on networking fundamentals using Cisco Packet Tracer. Feel free to fork and adapt!*

