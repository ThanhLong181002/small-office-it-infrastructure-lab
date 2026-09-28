# Network Design

## Network

- Network: 192.168.10.0/24
- Internal Network: CORP-LAN

## Server

- Hostname: SRV-DC01
- IP Address: 192.168.10.10
- OS: Windows Server 2022
- Roles:
  - Active Directory Domain Services
  - DNS
  - DHCP

## Domain

- Domain: corp.local
- NetBIOS: CORP

## DHCP

- Scope: 192.168.10.100 - 192.168.10.200
- Subnet Mask: 255.255.255.0
- DNS Server: 192.168.10.10

## Client

- Hostname: PC-CLIENT01
- OS: Windows 10 Pro
- Network: CORP-LAN
- IP: DHCP
- Domain: corp.local
