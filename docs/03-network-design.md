# Network Design

## Overview

The lab environment is designed with network segmentation to simulate a production environment.

The initial design separates server management traffic from application traffic.

VMware Workstation provides the virtual network layer.

## Networks

### Management Network

CIDR:

```text
192.168.10.0/24
```

VMware Network:

```text
VMnet2
```

Purpose:

* Server administration
* SSH access
* Monitoring
* Automation

DHCP is disabled.

Servers in this network use static IP addresses.

### Application Network

CIDR:

```text
192.168.20.0/24
```

VMware Network:

```text
VMnet3
```

Purpose:

* Application communication
* Internal services

DHCP is disabled.

Application servers will use static IP addresses.

### NAT Network

CIDR:

```text
192.168.254.0/24
```

VMware Network:

```text
VMnet8
```

Purpose:

* Internet access for lab servers
* Package installation
* External connectivity when required

This network uses VMware NAT and DHCP.

The NAT network is not part of the logical Management or Application network design.

## IP Allocation

| Host         | IP              | Network     | Status  |
| ------------ | --------------- | ----------- | ------- |
| `lab-git-01` | `192.168.10.10` | Management  | Active  |
| Monitoring   | `192.168.10.30` | Management  | Planned |
| App Server   | `192.168.20.10` | Application | Planned |
| Database     | `192.168.20.20` | Application | Planned |

The hostname `lab-git-01` currently identifies the Base Server. The Git server role will be introduced later.

## Current Server Network Configuration

### lab-git-01

| Interface | Network    | Address              | Configuration |
| --------- | ---------- | -------------------- | ------------- |
| `ens33`   | Management | `192.168.10.10/24`   | Static        |
| `ens37`   | VMware NAT | `192.168.254.128/24` | DHCP          |

Default gateway:

```text
192.168.254.2
```

The default route is intentionally configured through the NAT interface.

The Management interface does not have a default gateway.

## VMware Virtual Networks

| VMnet  | Type      | CIDR             | DHCP     | Purpose         |
| ------ | --------- | ---------------- | -------- | --------------- |
| VMnet2 | Host-Only | 192.168.10.0/24  | Disabled | Management      |
| VMnet3 | Host-Only | 192.168.20.0/24  | Disabled | Application     |
| VMnet8 | NAT       | 192.168.254.0/24 | Enabled  | Internet Access |

## Network Security

The Management network is used for administrative access.

On the current Base Server:

* Incoming traffic is denied by default.
* Outgoing traffic is allowed by default.
* SSH TCP/22 is allowed only from `192.168.10.0/24`.
* Routed traffic is currently disabled.

The Base Server is not intended to act as a router between the Management and Application networks.

## Future Network Evolution

As the environment grows, additional network controls may be introduced:

* Firewall rules between network segments
* Application-specific ports
* Database access restrictions
* Monitoring traffic
* Load balancing
* High Availability networking
* DNS infrastructure
* VLAN-like segmentation

These controls will be introduced based on actual application and infrastructure requirements.
