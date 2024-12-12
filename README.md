# Network-Design-for-Airport-CiscoPacket

This project is a network simulation for an airport's internal infrastructure, designed using Cisco Packet Tracer. The setup includes VLAN segmentation, inter-VLAN routing, DHCP configuration, access control, VPN functionality, and wireless access for guests. It allows secure and efficient connectivity across departments: Airport Authority, Flight Service, and Guest users, each with distinct network access policies.

## Table of Contents

- [Problem Statement](#problem-statement)
- [Project Overview](#project-overview)
- [Network Topology](#network-topology)
- [Components and Configuration](#components-and-configuration)
  - [Router](#router)
  - [Switches](#switches)
  - [DHCP Server](#dhcp-server)
  - [Access Point](#access-point)
  - [VPN Router](#vpn-router)
- [VLANs](#vlans)
- [Access Control Lists (ACLs)](#access-control-lists-acls)
- [VPN Functionality](#vpn-functionality)
- [IP Addressing Table](#ip-addressing-table)
- [Usage](#usage)

## Problem Statement

This project entails designing a network setup for an airport, which consists of three departments:

1) **Airport Authority**
2) **Flight Service Providers**
3) **Guests**

The Airport Authority maintains a dedicated server for flight management controls, accessible only to Flight Service Providers while being restricted from other systems. Guest users require secure wireless access to high-speed internet, shared across all departments, with access controlled via a common password. Guest users should not access the internal networks of the other departments. IP addresses should be assigned dynamically to users through DHCP.

The network configuration supports:
- **Airport Authority**: up to 20 users
- **Flight Service Providers**: up to 40 users
- **Guests**: a maximum of 100 users 

## Project Overview

The network project simulates an airport network with three main user groups:

1. **Airport Authority**: Handles airport management and flight control resources, including a dedicated server.
2. **Flight Service Providers**: Access to flight-related resources only.
3. **Guest Users**: Provided with internet access only, using a shared wireless access point with a common password.

Each department is allocated a separate VLAN, and access control is enforced to prevent unauthorized access to sensitive resources.

## Network Topology

The topology consists of a main router connected to four switches. Each switch serves a specific VLAN:
- **Switch 1 (VLAN 2)**: Airport Authority
- **Switch 2 (VLAN 3)**: Flight Service
- **Switch 3 & 4 (VLAN 4)**: Guest users

A DHCP server is connected to Switch 1 for dynamic IP allocation, and a VPN router is included for secure remote access to internal resources.

## Components and Configuration

### Router

- Handles inter-VLAN routing and applies access control policies.
- Configures **NAT** for internet access and maintains the **VPN connection** for secure remote access.
- Routes traffic between VLANs via subinterfaces on `GigabitEthernet0/0`.
- NAT and ACLs are used to restrict access for each VLAN.

### Switches

- Four switches support VLAN segmentation, with trunk links between them for inter-VLAN traffic.
- Each switch port is assigned to a specific VLAN to manage traffic based on department.

### DHCP Server

- Connected to Switch 1 and configured to allocate IPs for VLANs 2, 3, and 4.
- Ensures that each VLAN receives IP addresses within its designated subnet.

### Access Point

- Provides wireless internet access for guest users across all departments.
- Configured with a common password and SSID, allowing devices like laptops and smartphones to connect.

### VPN Router

- Manages secure connections to the airport’s internal network for authorized remote users.
- Configured to restrict VPN access to the Airport Authority VLAN, ensuring controlled access to sensitive resources.

## VLANs

Each VLAN corresponds to a department in the airport:
- **VLAN 2**: Airport Authority (192.168.2.0/24)
- **VLAN 3**: Flight Service Providers (192.168.3.0/24)
- **VLAN 4**: Guests (192.168.4.0/24)

Trunking using the **802.1Q protocol** is set up between the switches and router to allow traffic tagged with specific VLAN IDs to flow across the network.

## Access Control Lists (ACLs)

ACLs are configured to:
- Permit the Flight Service VLAN to access only specific resources within the Airport Authority VLAN.
- Deny guest access to Airport Authority and Flight Service resources, restricting them to internet access only.

## VPN Functionality

The VPN router allows authorized users to securely connect to the airport’s internal network from external locations. Using encrypted connections, VPN users can access the Airport Authority VLAN resources as if they were on-site.

## IP Addressing Table

| Component        | Interface           | IP Address      | VLAN ID |
|------------------|---------------------|-----------------|---------|
| Router           | Gig0/0.1            | 192.168.1.1     | VLAN 1  |
| Router           | Gig0/0.2            | 192.168.2.1     | VLAN 2  |
| Router           | Gig0/0.3            | 192.168.3.1     | VLAN 3  |
| Router           | Gig0/0.4            | 192.168.4.1     | VLAN 4  |
| DHCP Server      | FastEthernet0       | 192.168.2.2     | VLAN 2  |
| Airport Authority Server | Fast Ethernet0           | 192.168.2.3     | VLAN 2  |
| VPN Router       | -                   | 192.168.5.1     | VPN Network |


## Usage

1. Open the project in Cisco Packet Tracer.
2. Verify DHCP settings by checking IP allocation across VLANs.
3. Test ACLs by attempting to access restricted resources from different VLANs.
4. Test VPN access to ensure secure remote connectivity.
5. Connect a device to the access point to verify wireless access.

--- 

This README provides an overview for team members and collaborators to understand and replicate the setup. Make sure to tailor any additional configuration details specific to your Packet Tracer setup in the README for full documentation.
