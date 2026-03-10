# Day 9 — Inter-VLAN Routing
Date: March 10, 2026
Topic: Inter-VLAN Routing (Router on a Stick)
Stage: Stage 2 — Intermediate
Status: ✅ Completed

---

## What I Did Today
- Learned Inter-VLAN Routing theory fully
- Built Inter-VLAN Routing project in Packet Tracer
- Configured trunk and access ports on switch
- Configured subinterfaces on router
- Tested connectivity between all VLANs

---

## What is Inter-VLAN Routing?
Process of allowing different VLANs to
communicate with each other through a router.

Without Inter-VLAN Routing:
VLAN 10 cannot talk to VLAN 20 ❌
VLAN 20 cannot talk to VLAN 30 ❌

With Inter-VLAN Routing:
VLAN 10 talks through Router to VLAN 20 ✅
VLAN 20 talks through Router to VLAN 30 ✅

---

## Two Methods

Method 1 - Traditional
Each VLAN gets own physical cable to router.
Simple but wastes router ports.
Not practical for large networks.

Method 2 - Router on a Stick
All VLANs share ONE cable to router.
Router uses subinterfaces for each VLAN.
More efficient! Only needs one router port.
This is what we used!

---

## What is a Subinterface?
Virtual interface created inside one
physical interface.

Physical interface: Gig0/0 (one door)
Subinterfaces:
Gig0/0.10 = handles VLAN 10 traffic
Gig0/0.20 = handles VLAN 20 traffic
Gig0/0.30 = handles VLAN 30 traffic

Think of it like one highway divided
into separate lanes for each VLAN!

---

## What is a Trunk Port?
Special port that carries ALL VLAN traffic.

Normal port = carries ONE VLAN only
Trunk port  = carries ALL VLANs

Used between Switch and Router
so all VLAN traffic can travel
through one cable!

---

## What is 802.1Q / dot1q?
Standard that tags VLAN traffic.
Each packet gets a tag showing
which VLAN it belongs to.

PC in VLAN 10 sends data
Switch adds tag: This is VLAN 10!
Router reads tag and sends to
correct subinterface Gig0/0.10

---

## How It Works Step by Step
Step 1 = PC0 in VLAN 10 wants to talk to PC1 in VLAN 20
Step 2 = PC0 sends data to default gateway 192.168.10.1
Step 3 = Data travels through trunk port to router
Step 4 = Router receives data tagged as VLAN 10
Step 5 = Router routes data to VLAN 20
Step 6 = Router sends data out Gig0/0.20
Step 7 = Switch delivers data to PC1 in VLAN 20

---

## Network Layout We Built
Router (2911)
      |
    Switch
   /   |   \
 PC0  PC1  PC2
VLAN10 VLAN20 VLAN30

---

## IP Plan

VLAN 10 - IT Department
Router subinterface = 192.168.10.1
PC0 = 192.168.10.10
Gateway = 192.168.10.1

VLAN 20 - Office Staff
Router subinterface = 192.168.20.1
PC1 = 192.168.20.10
Gateway = 192.168.20.1

VLAN 30 - Management
Router subinterface = 192.168.30.1
PC2 = 192.168.30.10
Gateway = 192.168.30.1

---

## Cable Types Used
PC to Switch     = Copper Straight-Through
Switch to Router = Copper Straight-Through
(trunk port handles all VLANs on this cable)

---

## Switch Commands

# Create VLANs
en
conf t
vlan 10
name IT
exit
vlan 20
name OFFICE
exit
vlan 30
name MANAGEMENT
exit

# Set trunk port (switch to router)
interface fa0/1
switchport mode trunk
exit

# Set access port for PC0 (VLAN 10)
interface fa0/2
switchport mode access
switchport access vlan 10
exit

# Set access port for PC1 (VLAN 20)
interface fa0/3
switchport mode access
switchport access vlan 20
exit

# Set access port for PC2 (VLAN 30)
interface fa0/4
switchport mode access
switchport access vlan 30
exit

---

## Router Commands

# Turn on physical interface first!
en
conf t
interface gig0/0
no shutdown
exit

# Create subinterface for VLAN 10
interface gig0/0.10
encapsulation dot1q 10
ip address 192.168.10.1 255.255.255.0
exit

# Create subinterface for VLAN 20
interface gig0/0.20
encapsulation dot1q 20
ip address 192.168.20.1 255.255.255.0
exit

# Create subinterface for VLAN 30
interface gig0/0.30
encapsulation dot1q 30
ip address 192.168.30.1 255.255.255.0
exit

---

## PC IP Settings

PC0:
IP Address:      192.168.10.10
Subnet Mask:     255.255.255.0
Default Gateway: 192.168.10.1

PC1:
IP Address:      192.168.20.10
Subnet Mask:     255.255.255.0
Default Gateway: 192.168.20.1

PC2:
IP Address:      192.168.30.10
Subnet Mask:     255.255.255.0
Default Gateway: 192.168.30.1

---

## Verification Commands

# Check VLANs on switch
show vlan brief

# Check trunk port
show interfaces trunk

# Check subinterfaces on router
show ip interface brief

# Check routing table
show ip route

---

## Test Commands

# PC0 ping PC1 (VLAN 10 to VLAN 20)
ping 192.168.20.10

# PC0 ping PC2 (VLAN 10 to VLAN 30)
ping 192.168.30.10

# PC1 ping PC2 (VLAN 20 to VLAN 30)
ping 192.168.30.10

---

## Test Results
- PC0 ping PC1 across VLANs = Success ✅
- PC0 ping PC2 across VLANs = Success ✅
- PC1 ping PC2 across VLANs = Success ✅
- All VLANs talking through router = Success ✅

---

## Important Terms
VLAN         = virtual separate network
Inter-VLAN   = routing between VLANs
Trunk port   = carries all VLAN traffic
Access port  = carries one VLAN only
Subinterface = virtual router port per VLAN
802.1Q       = standard for tagging VLAN traffic
dot1q        = short name for 802.1Q
Encapsulation= wrapping data with VLAN tag
Router on stick = one cable handles all VLANs

---

## Real World Use
Company has 3 departments on same switch.
All separated by VLANs for security.
But IT needs to access Management server.
Inter-VLAN routing allows controlled access.
Router decides which VLANs can talk!

---

## Simple Summary
VLAN alone      = departments separated cannot talk
Inter-VLAN      = router allows controlled talking
Trunk port      = highway carrying all VLANs
Access port     = single lane road one VLAN only
Subinterface    = virtual router port for each VLAN
dot1q           = labels each packet with VLAN ID
Router on stick = one physical cable all VLANs

---

## Struggles
- Understanding trunk vs access ports
- Had to turn on physical interface first
  before subinterfaces would work
- Making sure encapsulation dot1q matches
  the correct VLAN number

---

## Tomorrow
Start NAT - Network Address Translation

---
Next Topic: Day 11 — NAT
Previous Topic: Day 9 — Inter-VLAN Routing Theory
