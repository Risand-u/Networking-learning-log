# Day 6 — Full Revision
Date: March 01, 2026
Topic: Revision of All Stage 1 Topics
Stage: Stage 1 — Beginner
Status: ✅ Completed

---

## What I Did Today
- Revised all topics learned so far
- Reviewed all projects built in Packet Tracer
- Strengthened understanding of all concepts
- Will upload DNS project tomorrow

---

## Quick Revision of Everything

### Topic 1 — Basic Network Setup
What it is:
Connecting devices together in a network

Key things:
- Router = connects networks together
- Switch = connects devices in same network
- Cable = Copper Straight-Through for different devices
- Cable = Copper Crossover for same devices

IP Addresses we used:
Router → 192.168.1.1
PC1    → 192.168.1.10
PC2    → 192.168.1.20

Security we added:
- VLANs to separate office and guest
- ACL rules to block unauthorized access

---

### Topic 2 — Subnetting
What it is:
Dividing one big network into smaller ones

Before subnetting:
192.168.1.0/24 = 254 devices all mixed together

After subnetting:
192.168.1.0/26   = IT Department  (62 devices)
192.168.1.64/26  = Office Staff   (62 devices)
192.168.1.128/26 = Management     (62 devices)

Important terms:
Network Address  = first IP, street name ❌
Broadcast        = last IP, notice board ❌
Usable Range     = IPs you can give devices ✅
Default Gateway  = router, first usable IP ✅

CIDR Cheat Sheet:
/24 = 254 devices
/25 = 126 devices
/26 = 62 devices
/27 = 30 devices
/28 = 14 devices
/30 = 2 devices

---

### Topic 3 — DHCP
What it is:
Automatically gives IP addresses to devices

DORA Process:
D = Discover  → PC asks for IP
O = Offer     → Server offers IP
R = Request   → PC accepts IP
A = Acknowledge → Server confirms

DHCP gives 4 things:
1. IP Address      → 192.168.1.11
2. Subnet Mask     → 255.255.255.192
3. Default Gateway → 192.168.1.1
4. DNS Server      → 192.168.1.50

Key commands:
ip dhcp excluded-address 192.168.1.1 192.168.1.10
ip dhcp pool IT-DEPARTMENT
network 192.168.1.0 255.255.255.192
default-router 192.168.1.1
dns-server 192.168.1.50

---

### Topic 4 — DNS
What it is:
Phone book of the internet
Converts website names to IP addresses

How it works:
You type google.com
DNS finds 142.250.180.46
Browser connects to that IP

DNS Record Types:
A Record    = name to IP
CNAME       = nickname to another name
MX Record   = email routing
PTR Record  = IP to name (reverse)

What I built:
DNS Server IP → 192.168.1.50
Records added:
company.com     → 192.168.1.50
www.company.com → 192.168.1.50

Key commands:
ip name-server 192.168.1.50
ping company.com
nslookup company.com

---

## All Projects Built So Far

Project 1 - Basic Network
- Router, Switch, 2 PCs
- VLANs and ACL rules
- Manual IP configuration
Status: ✅ Complete

Project 2 - Subnetting
- Router, 3 Switches, 6 PCs
- 3 department subnets
- Manual IP on router interfaces
Status: ✅ Complete

Project 3 - DHCP
- Same as subnetting
- Added DHCP server on router
- PCs get IPs automatically
Status: ✅ Complete

Project 4 - DNS
- Added DNS server to network
- Created DNS records
- PCs find websites by name
Status: ✅ Completed

---

## My GitHub Repos Status

network-security-lab
├── basic-network  ✅
├── subnetting     ✅
├── dhcp           ✅
└── dns            ✅

networking-roadmap
Stage 1:
✅ Basic network setup
✅ IP addressing
✅ VLANs
✅ ACL Firewall rules
✅ Basic ping testing
✅ Subnetting
✅ DHCP
✅ DNS basics

cybersecurity-notes
✅ Day 1 - Basic Network
✅ Day 2 - Subnetting
✅ Day 3 - DHCP
✅ Day 4 - Revision
✅ Day 5 - DNS Theory
✅ Day 6 - Full Revision

---

## Simple Summary of Everything

Router    = security guard, connects networks
Switch    = hallway, connects devices
IP        = home address of device
Subnet    = smaller network inside big network
DHCP      = automatic IP giver
DNS       = phone book of internet
Gateway   = door to outside network
Broadcast = notice board for everyone
Cache     = saved memory for speed
A Record  = converts name to IP address

---

## What is Coming Next
Stage 2 topics:
- Static and Dynamic Routing (OSPF RIP)
- Inter-VLAN Routing
- NAT
- VPN Setup
- Port Security
- Wireless Network Setup

---
Next Topic: Day 7 — Static and Dynamic Routing

