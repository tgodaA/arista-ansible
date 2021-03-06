# AVD_FABRIC

# Table of Contents
<!-- toc -->

- [Fabric Switches and Management IP](#fabric-switches-and-management-ip)
  - [Fabric Switches with inband Management IP](#fabric-switches-with-inband-management-ip)
- [Fabric Topology](#fabric-topology)
- [Fabric IP Allocation](#fabric-ip-allocation)
  - [Fabric Point-To-Point Links](#fabric-point-to-point-links)
  - [Point-To-Point Links Node Allocation](#point-to-point-links-node-allocation)
  - [Overlay Loopback Interfaces (BGP EVPN Peering)](#overlay-loopback-interfaces-bgp-evpn-peering)
  - [Loopback0 Interfaces Node Allocation](#loopback0-interfaces-node-allocation)
  - [VTEP Loopback VXLAN Tunnel Source Interfaces (Leafs Only)](#vtep-loopback-vxlan-tunnel-source-interfaces-leafs-only)
  - [VTEP Loopback Node allocation](#vtep-loopback-node-allocation)

<!-- toc -->
# Fabric Switches and Management IP

| POD | Type | Node | Management IP | Platform | Provisioned in CloudVision |
| --- | ---- | ---- | ------------- | -------- | -------------------------- |
| AVD_FABRIC | l3leaf | AVD-LEAF1A | 192.168.0.11/24 | vEOS-LAB | Not Available |
| AVD_FABRIC | l3leaf | AVD-LEAF1B | 192.168.0.12/24 | vEOS-LAB | Not Available |
| AVD_FABRIC | l3leaf | AVD-LEAF2A | 192.168.0.13/24 | vEOS-LAB | Not Available |
| AVD_FABRIC | l3leaf | AVD-LEAF2B | 192.168.0.14/24 | vEOS-LAB | Not Available |
| AVD_FABRIC | spine | AVD-SPINE1 | 192.168.0.1/24 | vEOS-LAB | Not Available |
| AVD_FABRIC | spine | AVD-SPINE2 | 192.168.0.2/24 | vEOS-LAB | Not Available |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

## Fabric Switches with inband Management IP
| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

# Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| l3leaf | AVD-LEAF1A | Ethernet1 | mlag_peer | AVD-LEAF1B | Ethernet1 |
| l3leaf | AVD-LEAF1A | Ethernet2 | mlag_peer | AVD-LEAF1B | Ethernet2 |
| l3leaf | AVD-LEAF1A | Ethernet3 | spine | AVD-SPINE1 | Ethernet2 |
| l3leaf | AVD-LEAF1A | Ethernet4 | spine | AVD-SPINE2 | Ethernet2 |
| l3leaf | AVD-LEAF1B | Ethernet3 | spine | AVD-SPINE1 | Ethernet3 |
| l3leaf | AVD-LEAF1B | Ethernet4 | spine | AVD-SPINE2 | Ethernet3 |
| l3leaf | AVD-LEAF2A | Ethernet1 | mlag_peer | AVD-LEAF2B | Ethernet1 |
| l3leaf | AVD-LEAF2A | Ethernet2 | mlag_peer | AVD-LEAF2B | Ethernet2 |
| l3leaf | AVD-LEAF2A | Ethernet3 | spine | AVD-SPINE1 | Ethernet4 |
| l3leaf | AVD-LEAF2A | Ethernet4 | spine | AVD-SPINE2 | Ethernet4 |
| l3leaf | AVD-LEAF2B | Ethernet3 | spine | AVD-SPINE1 | Ethernet5 |
| l3leaf | AVD-LEAF2B | Ethernet4 | spine | AVD-SPINE2 | Ethernet5 |

# Fabric IP Allocation

## Fabric Point-To-Point Links

| P2P Summary | Available Addresses | Assigned addresses | Assigned Address % |
| ----------- | ------------------- | ------------------ | ------------------ |
| 172.31.255.0/24 | 256 | 16 | 6.25 % |

## Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |
| AVD-LEAF1A | Ethernet3 | 172.31.255.1/31 | AVD-SPINE1 | Ethernet2 | 172.31.255.0/31 |
| AVD-LEAF1A | Ethernet4 | 172.31.255.3/31 | AVD-SPINE2 | Ethernet2 | 172.31.255.2/31 |
| AVD-LEAF1B | Ethernet3 | 172.31.255.5/31 | AVD-SPINE1 | Ethernet3 | 172.31.255.4/31 |
| AVD-LEAF1B | Ethernet4 | 172.31.255.7/31 | AVD-SPINE2 | Ethernet3 | 172.31.255.6/31 |
| AVD-LEAF2A | Ethernet3 | 172.31.255.9/31 | AVD-SPINE1 | Ethernet4 | 172.31.255.8/31 |
| AVD-LEAF2A | Ethernet4 | 172.31.255.11/31 | AVD-SPINE2 | Ethernet4 | 172.31.255.10/31 |
| AVD-LEAF2B | Ethernet3 | 172.31.255.13/31 | AVD-SPINE1 | Ethernet5 | 172.31.255.12/31 |
| AVD-LEAF2B | Ethernet4 | 172.31.255.15/31 | AVD-SPINE2 | Ethernet5 | 172.31.255.14/31 |

## Overlay Loopback Interfaces (BGP EVPN Peering)

| Overlay Loopback Summary | Available Addresses | Assigned addresses | Assigned Address % |
| ------------------------ | ------------------- | ------------------ | ------------------ |
| 192.168.255.0/24 | 256 | 6 | 2.35 % |

## Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| AVD_FABRIC | AVD-LEAF1A | 192.168.255.3/32 |
| AVD_FABRIC | AVD-LEAF1B | 192.168.255.4/32 |
| AVD_FABRIC | AVD-LEAF2A | 192.168.255.5/32 |
| AVD_FABRIC | AVD-LEAF2B | 192.168.255.6/32 |
| AVD_FABRIC | AVD-SPINE1 | 192.168.255.1/32 |
| AVD_FABRIC | AVD-SPINE2 | 192.168.255.2/32 |

## VTEP Loopback VXLAN Tunnel Source Interfaces (Leafs Only)

| VTEP Loopback Summary | Available Addresses | Assigned addresses | Assigned Address % |
| --------------------- | ------------------- | ------------------ | ------------------ |
| 192.168.254.0/24 | 256 | 4 | 1.57 % |

## VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
| AVD_FABRIC | AVD-LEAF1A | 192.168.254.3/32 |
| AVD_FABRIC | AVD-LEAF1B | 192.168.254.3/32 |
| AVD_FABRIC | AVD-LEAF2A | 192.168.254.5/32 |
| AVD_FABRIC | AVD-LEAF2B | 192.168.254.5/32 |
