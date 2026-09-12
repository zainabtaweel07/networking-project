# networking-project
# Enterprise Network Design and Implementation

## Overview
This project is a multi-site enterprise network simulated in Cisco Packet Tracer. It connects 1 Headquarters (HQ) location with 7 regional branches to centralize communication and network management.

**Key goals:**
- Allocate IP addresses efficiently using VLSM.
- Share centralized network services hosted at HQ.
- Enable automatic route sharing across sites using OSPF.

## Network Structure

- **WAN (Hub & Spoke):** HQ acts as the main hub connected directly to each branch router using serial connections.
- **LAN (Star Topology):** End devices in each office connect directly to a central switch. Wi-Fi points use WPA2-PSK encryption.

## IP Subnetting Summary

| Network Area | Subnet Mask | Host Capacity | Notes |
|---|---|---|---|
| HQ LAN | `255.255.255.128` (`/25`) | Up to 126 hosts | `192.168.8.0/25` network |
| Branch LANs (7 sites) | `255.255.255.0` (`/24`) | Up to 254 hosts per site | Subnets `192.168.1.0` through `192.168.7.0` |
| WAN Links | `255.255.255.252` (`/30`) | 2 usable IPs per link | Point-to-point connections |

## Centralized Servers (HQ)

All primary network servers are located in the HQ LAN (`192.168.8.0/25`):

- **DHCP** (`192.168.8.2`): Assigns IP addresses to all devices automatically.
- **Web** (`192.168.8.3`): Secure HTTPS web server.
- **DNS** (`192.168.8.4`): Translates web addresses into IP addresses.
- **FTP** (`192.168.8.5`): File transfer and storage server.
- **Mail** (`192.168.8.6`): Handles internal emails using SMTP and POP3.

## Essential Configurations

- **Router Security:** Secured with console, privilege, and encrypted secret passwords.
- **Dynamic Routing:** OSPF Area 1 runs across all routers. LAN interfaces are set to passive to reduce network traffic.
- **DHCP Relay:** Branch routers use `ip helper-address 192.168.8.2` to fetch IP addresses from HQ.

## Tools Used
- Cisco Packet Tracer

## File
- `network-project.pkt` — the full simulation file
