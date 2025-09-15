# DHCP Configuration in Cisco Packet Tracer

This guide explains how to configure a Cisco Router as a DHCP server in **Cisco Packet Tracer**, assign IPs automatically to PCs/Servers, and troubleshoot common issues.

---

## 🖥️ Network Topology
Example setup:
- Router (DHCP Server)
- Switches
- PCs and Servers connected to the switches

Connections:
- Router **Fa0/0** → Switch1 → PC0, PC1, server1
- Router **Fa0/1** → Switch2 → PC3, PC4, server2

---

## ⚙️ Steps to Configure DHCP

### 1. On the Router
Enter global configuration mode and create the DHCP pool:

```bash
enable
configure terminal

! Exclude reserved addresses (gateway, servers, printers, etc.)
ip dhcp excluded-address 192.168.1.1 192.168.1.10

! Create DHCP pool
ip dhcp pool LANPOOL
 network 192.168.1.0 255.255.255.0
 default-router 192.168.1.1
 dns-server 8.8.8.8
 exit

! Configure LAN interface
interface fastEthernet0/0
 ip address 192.168.1.1 255.255.255.0
 no shutdown
exit

end
write memory
