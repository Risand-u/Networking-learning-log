# Day 11 — NAT (Network Address Translation)
Date: March 21, 2026
Topic: NAT - Network Address Translation
Stage: Stage 2 — Intermediate
Status: ✅ Completed

--- 

## What I Did Today
- Learned full NAT theory
- Understood different types of NAT
- Understood why NAT is used in real world
- Will build NAT project in Packet Tracer next

--- 

## What is NAT?
NAT stands for Network Address Translation.
It is a method that allows multiple devices
on a private network to share one single
public IP address to access the internet.

Think of it like an office building.
The building has one main address
but many people work inside it.
When someone sends a letter from inside
it shows the building address not
the individual person's address!

Without NAT every device would need
its own unique public IP address.
There are not enough public IPs
for every device in the world!
NAT solves this problem!

---

## Why Do We Need NAT?

Problem:
The internet uses IPv4 addresses.
IPv4 only has about 4 billion addresses.
There are more than 4 billion devices
connected to internet today!
We ran out of public IP addresses!

Solution:
NAT allows thousands of devices to
share one single public IP address.
Private IP addresses are used inside
the network and NAT converts them
to public IP when accessing internet.

---

## Private vs Public IP Addresses

Private IP addresses are used INSIDE networks.
They are free to use and not routable on internet.
Public IP addresses are used on the INTERNET.
They are unique and registered.

Private IP ranges:
10.0.0.0    to 10.255.255.255    (Class A)
172.16.0.0  to 172.31.255.255   (Class B)
192.168.0.0 to 192.168.255.255  (Class C)

Public IP addresses:
Everything else that is not private!
Assigned by ISP (Internet Service Provider)
Must be unique across entire internet!

Example:
Your home network uses 192.168.1.x
This is private IP
Your ISP gives you one public IP like 203.45.67.89
NAT converts 192.168.1.x to 203.45.67.89
when you access internet!

---

## Three Types of NAT

Type 1 - Static NAT
One private IP maps to one public IP permanently.
Same private IP always gets same public IP.
Used for servers that need to be
accessible from internet.

Example:
192.168.10.5 always maps to 203.45.67.100
Anyone on internet can reach 203.45.67.100
and it always goes to 192.168.10.5!

Good for:
Web servers
Email servers
FTP servers
Any server that needs permanent public IP

Type 2 - Dynamic NAT
Pool of public IPs shared among private IPs.
Private IP gets any available public IP
from the pool when needed.
When done public IP goes back to pool.

Example:
Pool of public IPs: 203.45.67.100 to 203.45.67.110
PC1 gets 203.45.67.100 when browsing
PC2 gets 203.45.67.101 when browsing
When PC1 stops browsing 203.45.67.100
goes back to pool for others to use!

Good for:
When you have multiple public IPs
but fewer than number of users

Type 3 - PAT (Port Address Translation)
Also called NAT Overload
Most common type used everywhere!
Many private IPs share ONE single public IP
using different port numbers to track connections.

Example:
PC1 192.168.1.10 browsing = public IP 203.45.67.89 port 1234
PC2 192.168.1.11 browsing = public IP 203.45.67.89 port 5678
PC3 192.168.1.12 browsing = public IP 203.45.67.89 port 9012
All three use SAME public IP but different ports!
Router tracks which port belongs to which PC!

Good for:
Home networks
Small offices
Anywhere with one public IP!
This is what your home router uses!

---

## How NAT Works Step by Step

Example using PAT (most common):

Step 1 = PC1 (192.168.1.10) wants to visit google.com
Step 2 = PC1 sends packet to router
         Source IP: 192.168.1.10 Port: 54321
Step 3 = Router replaces private IP with public IP
         Source IP: 203.45.67.89 Port: 1234
         Router saves this translation in NAT table!
Step 4 = Packet goes to Google
Step 5 = Google sends reply to 203.45.67.89 Port 1234
Step 6 = Router checks NAT table
         Port 1234 = belongs to 192.168.1.10!
Step 7 = Router forwards reply to PC1 192.168.1.10
Step 8 = PC1 receives Google page! ✅

---

## NAT Table
Router keeps a NAT table to track all connections:

Inside Local    Inside Global    Outside
192.168.1.10:54321  203.45.67.89:1234  Google IP
192.168.1.11:54322  203.45.67.89:5678  Facebook IP
192.168.1.12:54323  203.45.67.89:9012  YouTube IP

Inside Local  = private IP of device
Inside Global = public IP used on internet
Outside       = destination on internet

---

## NAT Terms

Inside Local
= Private IP address of device inside network
= Example: 192.168.1.10
= This is what device thinks its address is

Inside Global
= Public IP address seen by internet
= Example: 203.45.67.89
= This is what internet sees

Outside Global
= IP address of destination on internet
= Example: Google's IP 142.250.80.46

Outside Local
= How outside destination appears to inside network
= Usually same as Outside Global

---

## NAT Commands

Step 1 - Define inside and outside interfaces:
interface gig0/0
ip nat inside
exit
interface gig0/1
ip nat outside
exit

Step 2 - Create access list to define
which IPs to translate:
access-list 1 permit 192.168.0.0 0.0.255.255

Step 3 - Enable PAT using outside interface:
ip nat inside source list 1 interface gig0/1 overload

Step 4 - Verify NAT:
show ip nat translations
show ip nat statistics

---

## Verification Commands

show ip nat translations
= shows current NAT table
= shows all active translations

show ip nat statistics
= shows how many translations
= shows inside and outside interfaces

debug ip nat
= shows NAT happening in real time
= useful for troubleshooting

clear ip nat translation *
= clears all NAT translations
= useful for testing

---

## Important Terms
NAT     = Network Address Translation
PAT     = Port Address Translation
Overload= another name for PAT
Inside  = your private network side
Outside = internet side
Static  = one to one permanent mapping
Dynamic = pool of public IPs shared
Port    = number used to track connections
ISP     = Internet Service Provider
Public IP = unique address on internet
Private IP = address used inside network

---

## Advantages of NAT
Security
= Private IPs are hidden from internet
= Hackers cannot directly reach
  internal devices
= Adds layer of security!

IP Conservation
= Thousands of devices share one public IP
= Solves IPv4 address shortage problem

Flexibility
= Can change internal IP scheme
  without affecting public IP
= Easy to reorganize internal network

---

## Disadvantages of NAT
Performance
= Router has to translate every packet
= Adds small delay to connections

Some apps dont work well
= Some applications need direct IP connection
= VoIP and gaming can have issues
= Needs special configuration

Troubleshooting is harder
= Hard to track which device
  is making which connection
= Need to check NAT table

---

## Real World Use

Home Network:
Your home router uses PAT!
All your devices (phone, laptop, TV)
share ONE public IP given by ISP!
Router tracks all connections using ports!

Company Network:
Company has 500 employees
ISP gives company 5 public IPs
NAT allows all 500 employees to
share those 5 public IPs!
Saves money on public IP costs!

Web Server:
Company has web server at 192.168.1.100
Uses Static NAT to map to public IP
So internet users can access website!

---

## Simple Summary
NAT     = translates private IP to public IP
PAT     = many devices share one public IP
Static  = one private to one public permanent
Dynamic = pool of public IPs shared
Inside  = your network side
Outside = internet side
Overload= PAT with one public IP
Port    = used to track multiple connections
NAT table = router tracks all translations

---

## What is Coming Next
Build NAT project in Packet Tracer
Configure PAT on router
Test internet access from private network

---
Next Topic: Day 12 — NAT Project
Previous Topic: Day 10 — Inter-VLAN Routing Project
