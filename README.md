# 🧠 Campus Inter-VLAN Network Design (Cisco Packet Tracer)

> A complete simulation of an enterprise-level campus LAN with VLANs, inter-VLAN routing, DHCP, DNS, FTP/HTTP services, spanning tree protocol, and ACLs — designed in Cisco Packet Tracer.

---

## 🎯 Objectives

- Implement **VLANs** for departmental segmentation (Sales & HR)
- Use **Router-on-a-Stick** for Inter-VLAN routing
- Configure **DHCP** and **DNS** on a dedicated server
- Serve **FTP/HTTP** resources internally
- Apply **STP (Spanning Tree Protocol)** to prevent loops
- Enforce **Access Control Lists (ACLs)** for security

---

## 🧰 Tools & Devices

- **Cisco Packet Tracer**
- 2x L2 Switches (Switch0 & Switch1)
- 1x Router (with subinterfaces)
- 1x Server (DHCP, DNS, HTTP, FTP)
- Multiple PCs

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

- **VLANs:** Sales (10), HR (20)
- **Trunks:** Switch-to-router and switch-to-switch
- **Router-on-a-Stick:** Subinterfaces with `.10` & `.20` for routing
- **DHCP Relay:** `ip helper-address` to forward requests
- **STP:** `spanning-tree mode rapid-pvst`
- **ACLs:** To restrict HTTP access to server

---

## 🔐 Services Configured on Server

- **DHCP:** Address pools for both VLANs
- **DNS:** Internal name resolution
- **HTTP/FTP:** File server for internal access

---

## ⚠️ Challenges & Fixes

### 🔴 DHCP Not Working on PCs (Switch1)
- **Root Cause:** Server was connected to Switch0. PCs on Switch1 didn’t receive broadcasts due to VLAN isolation.
- **Fix:** Verified VLANs allowed on trunk & spanning-tree state. Ensured correct `ip helper-address` on router.

### 🔴 VLAN 20 Couldn’t Access HTTP
- **Root Cause:** Access list denied VLAN 20 before allowing it.
- **Fix:** Reordered ACL to allow VLAN 20 **before** deny rule and fixed subnet typo (`192.169.x.x` → `192.168.x.x`)

---

## 📸 Artifacts

Folder | Content
-------|--------
`/screenshots/` | VLAN tables, router configs, DHCP success, ping tests
`/configs/`     | CLI outputs via `show vlan brief`, `show int trunk`, etc.
`/topology/`    | Network diagram (before/after)

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
🔗 [LinkedIn](https://linkedin.com/in/your-profile)  
📁 [Portfolio](https://github.com/yourusername)

---

📌 *This project was developed as part of my self-study on networking fundamentals using Cisco Packet Tracer. Feel free to fork and adapt!*

