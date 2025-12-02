# Network-Security
Group 5 Network Security Project


1. Project Overview

This project implements a complete enterprise-style network security environment using pfSense Firewall, Suricata IDS/IPS, OpenVPN, and segregated network zones (LAN, DMZ, and Remote VPN).
The goal is to demonstrate secure network segmentation, intrusion detection, VPN connectivity, NAT behavior, and penetration testing techniques in a fully controlled lab environment.

2. Network Topology Summary

The topology consists of three major zones connected through pfSense:

LAN – 192.168.7.0/24

Used for internal clients and security testing.
Devices:

Kali Linux Workstation – 192.168.7.102

Windows 10 Workstation – 192.168.7.101

DMZ – 192.168.8.0/24

Used for externally accessible services.
Devices:

Ubuntu Server (Web/SSH) – 192.168.8.100

Remote VPN Network – 10.8.0.0/24

Used to simulate an external user securely connecting into the enterprise network.
Devices:

Windows OpenVPN Client – 10.8.0.2

All remote VPN traffic enters pfSense via UDP 1194, then is routed to appropriate LAN/DMZ hosts.

Upstream Connectivity

pfSense receives Internet access using VirtualBox NAT (Adapter 1) on WAN (em0).

Internal networks use LAN (em1) and OPT1 (em2).

3. pfSense Configuration Summary
Interfaces

WAN (em0) → VirtualBox NAT

LAN (em1) → Internal LAN network 192.168.7.0/24

OPT1 (em2) → DMZ 192.168.8.0/24

Firewall Rules

LAN → Allow internal outbound traffic

OPT1 (DMZ) → Restricted inbound, controlled outbound

WAN → Block all unsolicited inbound traffic

VPN → Allow authenticated OpenVPN clients

NAT

Outbound NAT configured for LAN and DMZ

NAT reflection disabled for security

Port forwarding configured for testing web access on DMZ server

4. Suricata IDS/IPS

Suricata is enabled in Inline IPS mode on both LAN and DMZ interfaces.

Rule sets enabled:

Emerging Threats Open Rules

GPLv2 Community Rules

Suricata actively blocks malicious patterns such as:

SYN flood indicators

Port scans

Invalid TCP flags

SSH brute force

Web exploit attempts

All alerts and blocks were captured and documented.

5. OpenVPN Configuration

Mode: Remote Access (User Auth + Certs)

Protocol: UDP 1194

Tunnel Network: 10.8.0.0/24

Windows Client Assigned IP: 10.8.0.2

Exported using pfSense’s OpenVPN Client Export Utility

Verified connectivity by accessing:

LAN machines

DMZ web server

pfSense GUI (expected TLS warning due to self-signed cert)



the pfsense.ova contains all the required configurations, please import it and follow the pdf
