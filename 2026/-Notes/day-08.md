# Day 9 — Inter-VLAN Routing Theory
Date: March 04, 2026
Topic: Inter-VLAN Routing
Stage: Stage 2 — Intermediate
Status: 📖 Currently Learning

---

## What I Did Today
- Learned Inter-VLAN Routing theory
- Understood difference between trunk and access ports
- Understood Router on a Stick concept
- Will build project in Packet Tracer next

---

## What is a VLAN?
VLAN stands for Virtual Local Area Network.
Separates one physical network into multiple
virtual networks.

One physical switch can have:
VLAN 10 → IT Department
VLAN 20 → Office Staff
VLAN 30 → Management

Think of it like walls inside a building.
Each department separated from others.

---

## The Problem With VLANs
VLANs are great for separation but by default
they cannot talk to each other!

VLAN 10 PC → cannot reach → VLAN 20 PC ❌

Sometimes departments need to communicate.
Inter-VLAN Routing fixes this!

---

## What is Inter-VLAN Routing?
Process of allowing different VLANs to
communicate with each other through a router.

Without Inter-VLAN Routing:
VLAN 10 ❌ VLAN 20 ❌ VLAN 30

With Inter-VLAN Routing:
VLAN 10 ✅ Router ✅ VLAN 20 ✅ VLAN 30

---

## Two Methods

Method 1 — Traditional
Each VLAN gets its own physical cable
to a separate router interface.
Simple but uses too many router ports!
Not practical for large networks.

Method 2 — Router on a Stick
All VLANs share ONE cable to router.
Router uses subinterfaces for each VLAN.
More efficient! Only needs one router port.
This is what we will use!

---

## What is a Subinterface?
A virtual interface created inside one
physical interface.

Physical interface: Gig0/0 (one door)
Subinterfaces:
Gig0/0.10 → handles VLAN 10 traffic
Gig0/0.20 → handles VLAN 20 traffic
Gig0/0.30 → handles VLAN 30 traffic

---

## What is a Trunk Port?
Special port that carries traffic from ALL VLANs.

Normal port = carries ONE VLAN traffic
Trunk port  = carries ALL VLAN traffic

Think of it like:
Normal port = one lane road
Trunk port  = highway with multiple lanes

---

## What is 802.1Q?
Standard that tags VLAN traffic so router
knows which VLAN each packet belongs to.

PC in VLAN 10 sends data
Switch adds tag: This is VLAN 10 traffic
Router receives tagged data
Router sends to correct subinterface

---

## How It Works Step by Step
Step 1 → PC0 in VLAN 10 wants to talk to PC2 in VLAN 20
Step 2 → PC0 sends data to default gateway
Step 3 → Router receives data tagged as VLAN 10
Step 4 → Router routes data to VLAN 20
Step 5 → Router sends data out Gig0/0.20
Step 6 → Switch delivers data to PC2 in VLAN 20

---

## Switch Commands
# Create VLANs
vlan 10
name IT
vlan 20
name OFFICE
vlan 30
name MANAGEMENT

# Set trunk port (switch to router)
interface fa0/1
switchport mode trunk

# Set access port (switch to PC)
interface fa0/2
switchport mode access
switchport access vlan 10

---

## Router Commands
# Create subinterfaces
interface gig0/0.10
encapsulation dot1q 10
ip address 192.168.10.1 255.255.255.0

interface gig0/0.20
encapsulation dot1q 20
ip address 192.168.20.1 255.255.255.0

interface gig0/0.30
encapsulation dot1q 30
ip address 192.168.30.1 255.255.255.0

---

## Important Terms
VLAN         = virtual separate network
Inter-VLAN   = routing between VLANs
Trunk port   = carries all VLAN traffic
Access port  = carries one VLAN traffic
Subinterface = virtual interface inside physical one
802.1Q       = standard for tagging VLAN traffic
dot1q        = short name for 802.1Q
Encapsulation= wrapping data with VLAN tag

---

## Real World Use
Company has 3 departments on same switch.
IT needs to access Management server.
Inter-VLAN routing allows controlled access.
Router controls which VLANs can talk.
Very important for network security!

---

## Simple Summary
VLAN alone       = departments separated
Inter-VLAN       = router allows communication
Trunk port       = switch port for all VLANs
Access port      = switch port for one VLAN
Subinterface     = virtual router port per VLAN
dot1q            = tags traffic with VLAN ID
Router on stick  = one cable handles all VLANs

---

## Struggles Today
- Understanding difference between
  trunk and access ports

  
- Understanding subinterfaces concept

---


