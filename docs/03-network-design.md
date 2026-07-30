# Network Design

## Overview

The lab environment is designed with network segmentation to simulate a production environment.

## Networks

### Management Network

CIDR:
192.168.10.0/24

Purpose:
- Server administration
- SSH access
- Monitoring
- Automation


### Application Network

CIDR:
192.168.20.0/24

Purpose:
- Application communication
- Internal services


## IP Allocation

| Host | IP | Network |
|---|---|---|
| GitLab | 192.168.10.10 | Management |
| Monitoring | 192.168.10.30 | Management |
| App Server | 192.168.20.10 | Application |
| Database | 192.168.20.20 | Application |
