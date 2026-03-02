# Day 7 — Static and Dynamic Routing
Date: March 02, 2026
Topic: Static and Dynamic Routing
Stage: Stage 2 — Intermediate
Status: 📖 Currently Learning

---

## What I Did Today
- Started Stage 2 of networking roadmap
- Learning Static and Dynamic Routing
- Building a 3 router network in Packet Tracer

---

## What is Routing?

Routing is how routers decide where to send data.
In our previous projects router already knew about
directly connected networks.

But what if we have multiple routers?
Each router needs to know how to reach
other networks. That is what routing solves!

---

## Two Types of Routing

### Static Routing
You manually tell the router which way to send traffic.
Like giving someone written directions.

Good for:
- Small networks
- Simple setups
- When routes never change

Bad for:
- Large networks
- When routes change often
- Takes time to configure manually

### Dynamic Routing (OSPF/RIP)
Routers automatically learn routes from each other.
Like a GPS that finds best route automatically.

Good for:
- Large networks
- When routes change often
- Automatic updates

Bad for:
- Uses more router resources
- More complex to understand

---

## What We Are Building

A network with 3 routers connected together:

PC0 --- Switch1 --- Router1 --- Router2 --- Router3 --- Switch2 --- PC1

PC0 and PC1 are on different networks.
We will make them talk using routing!

---

## Network IP Plan

Left side network:
PC0         → 192.168.1.10
Switch1     → no IP needed
Router1 Gig0/0 → 192.168.1.1

Link between Router1 and Router2:
Router1 Gig0/1 → 10.0.0.1
Router2 Gig0/0 → 10.0.0.2

Link between Router2 and Router3:
Router2 Gig0/1 → 10.0.1.1
Router3 Gig0/0 → 10.0.1.2

Right side network:
Router3 Gig0/1 → 192.168.2.1
Switch2     → no IP needed
PC1         → 192.168.2.10

---

## Cable Types Used

Copper Straight-Through:
- PC to Switch
- Switch to Router

Copper Cross-Over:
- Router to Router directly

---

## Simple Summary
Routing   = deciding where to send data
Static    = manual routes, you configure them
Dynamic   = automatic routes, routers learn themselves
OSPF      = most common dynamic routing protocol
Router    = uses routing table to forward data
Route     = path data takes to reach destination

---

Then configure OSPF dynamic routing

---
Next Topic: Day 8 — Routing Project Continued
Previous Topic: Day 6 — Full Revision
