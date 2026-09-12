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

## LAN Addressing Table

| # | Site | Network ID | Subnet Mask | Range | Default Gateway | Broadcast Address |
|---|---|---|---|---|---|---|
| 1 | Headquarters (Amman) | 172.16.0.0 /25 | 255.255.255.128 | 172.16.0.1 – 172.16.0.126 | 172.16.0.1 | 172.16.0.127 |
| 2 | North Regional Office (Irbid) | 172.16.0.128 /25 | 255.255.255.128 | 172.16.0.129 – 172.16.0.254 | 172.16.0.129 | 172.16.0.255 |
| 3 | South Regional Office (Aqaba) | 172.16.1.0 /25 | 255.255.255.128 | 172.16.1.1 – 172.16.1.126 | 172.16.1.1 | 172.16.1.127 |
| 4 | East Regional Office (Zarqa) | 172.16.1.128 /25 | 255.255.255.128 | 172.16.1.129 – 172.16.1.254 | 172.16.1.129 | 172.16.1.255 |
| 5 | West Regional Office (Al Salt) | 172.16.2.0 /25 | 255.255.255.128 | 172.16.2.1 – 172.16.2.126 | 172.16.2.1 | 172.16.2.127 |
| 6 | Data Recovery Centre (Madaba) | 172.16.2.128 /25 | 255.255.255.128 | 172.16.2.129 – 172.16.2.254 | 172.16.2.129 | 172.16.2.255 |
| 7 | Customer Support Centre (Mafraq) | 172.16.3.0 /25 | 255.255.255.128 | 172.16.3.1 – 172.16.3.126 | 172.16.3.1 | 172.16.3.127 |
| 8 | Training Centre (Karak) | 172.16.3.128 /25 | 255.255.255.128 | 172.16.3.129 – 172.16.3.254 | 172.16.3.129 | 172.16.3.255 |

## WAN Addressing Table

| # | Link | Network ID | Subnet Mask | HQ-Side IP | Branch-Side IP |
|---|---|---|---|---|---|
| 1 | HQ–Irbid | 209.165.201.0 /30 | 255.255.255.252 | 209.165.201.1 | 209.165.201.2 |
| 2 | HQ–Aqaba | 209.165.201.4 /30 | 255.255.255.252 | 209.165.201.5 | 209.165.201.6 |
| 3 | HQ–Zarqa | 209.165.201.8 /30 | 255.255.255.252 | 209.165.201.9 | 209.165.201.10 |
| 4 | HQ–Al Salt | 209.165.201.12 /30 | 255.255.255.252 | 209.165.201.13 | 209.165.201.14 |
| 5 | HQ–Madaba | 209.165.201.16 /30 | 255.255.255.252 | 209.165.201.17 | 209.165.201.18 |
| 6 | HQ–Mafraq | 209.165.201.20 /30 | 255.255.255.252 | 209.165.201.21 | 209.165.201.22 |
| 7 | HQ–Karak | 209.165.201.24 /30 | 255.255.255.252 | 209.165.201.25 | 209.165.201.26 |

## Centralized Servers (HQ)

All primary network servers are located in the HQ LAN (`172.16.0.0/25`):

- **DHCP** (`172.16.0.10`): Assigns IP addresses to all devices automatically.
- **Web** (`172.16.0.20`): Secure HTTPS web server.
- **DNS** (`172.16.0.30`): Translates web addresses into IP addresses.
- **FTP** (`172.16.0.40`): File transfer and storage server.
- **Mail** (`172.16.0.50`): Handles internal emails using SMTP and POP3.

## Essential Configurations

- **Router Security:** Secured with console, privilege, and encrypted secret passwords.
- **Dynamic Routing:** OSPF Area 1 runs across all routers. LAN interfaces are set to passive to reduce network traffic.
- **DHCP Relay:** Branch routers use `ip helper-address 172.16.0.10` to fetch IP addresses from HQ.

## Tools Used
- Cisco Packet Tracer

## File
- `network-project.pkt` — the full simulation file
