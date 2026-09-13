# Base Server

## Overview

The Base Server is the clean and generic operating system foundation for the lab environment.

The goal is to provide a stable, reusable and production-oriented server baseline before installing role-specific software.

## Server

| Item           | Value                     |
| -------------- | ------------------------- |
| Hostname       | `lab-git-01`              |
| OS             | Ubuntu Server 22.04.5 LTS |
| Kernel         | `5.15.0-94-generic`       |
| Architecture   | x86-64                    |
| Virtualization | VMware Workstation        |
| vCPU           | 2                         |
| RAM            | 4 GB                      |
| Disk           | 40 GB                     |
| Boot Mode      | UEFI                      |

## Network

### Management Interface

| Item            | Value              |
| --------------- | ------------------ |
| Interface       | `ens33`            |
| Network         | Management-Lab     |
| IP              | `192.168.10.10/24` |
| Address Type    | Static             |
| Default Gateway | None               |

### NAT Interface

| Item            | Value                |
| --------------- | -------------------- |
| Interface       | `ens37`              |
| Network         | VMware NAT           |
| IP              | DHCP                 |
| Current IP      | `192.168.254.128/24` |
| Default Gateway | `192.168.254.2`      |

The default route is intentionally configured through the NAT interface.

The Management network does not provide the default gateway.

## Storage

The server uses LVM.

```text
40 GB Disk
└── /dev/sda
    ├── /dev/sda1
    ├── /dev/sda2 → /boot
    └── /dev/sda3 → LVM PV
        └── ubuntu-vg
            └── ubuntu-lv → /
```

Current LVM capacity:

| Item         |       Value |
| ------------ | ----------: |
| Volume Group | `ubuntu-vg` |
| PVs          |           1 |
| LVs          |           1 |
| VG Size      |      ~38 GB |
| LV Size      |      ~19 GB |
| VG Free      |      ~19 GB |

The available VG space can be used later to extend the root filesystem without adding another disk.

## Base Packages

The following common administration and troubleshooting tools were installed:

* `curl`
* `wget`
* `vim`
* `nano`
* `htop`
* `tree`
* `unzip`
* `zip`
* `net-tools`
* `dnsutils`
* `lsof`
* `jq`
* `ca-certificates`

Role-specific software such as Git, Docker, Jenkins, Zabbix Agent and application-specific services is intentionally excluded from the Base Server.

## SSH Baseline

Effective SSH configuration:

```text
Port                  22
PermitRootLogin       without-password
PubkeyAuthentication  yes
PasswordAuthentication yes
```

Root SSH login using a password is disabled.

Password authentication for regular users remains enabled temporarily. SSH key-based administration will be introduced as part of the later security hardening stage.

## Firewall

UFW is enabled.

Default policy:

```text
Incoming → deny
Outgoing → allow
Routed   → disabled
```

SSH is allowed only from the Management network:

```text
192.168.10.0/24 → TCP/22
```

Firewall logging is enabled at low level.

The server is not intended to act as a router between the Management and Application networks.

## Time Synchronization

System time synchronization is enabled and healthy.

```text
systemd-timesyncd
NTP synchronized: yes
Timezone: UTC
```

UTC is used as the server timezone to provide consistent timestamps across the lab environment.

## System Updates

The system was updated before finalizing the Base Server.

Automatic security updates are enabled through `unattended-upgrades`.

Security repositories are included in the allowed update origins.

## System Services

At Base Server finalization:

* No failed systemd services were present.
* SSH was active.
* Network configuration was active.
* DNS resolution was active.
* Time synchronization was active.
* VMware integration tools were active.

## Base Server Principles

The Base Server intentionally remains generic.

The following principles are used:

1. Keep the OS clean and stable.
2. Install common administration tools only.
3. Install role-specific software when the server role is defined.
4. Avoid unnecessary aggressive hardening before the provisioning model is established.
5. Use network segmentation from the beginning.
6. Keep Management and Application networks logically separated.
7. Create a reusable clean state before cloning or snapshotting.

## Snapshot Strategy

After final verification, this server will be captured as the initial clean Base Server snapshot.

Proposed snapshot name:

```text
01-clean-ubuntu-22.04-base
```

The snapshot represents the validated operating-system baseline and should be used as a rollback point before major role-specific changes.

A Golden Image/Template and a Snapshot are considered different concepts:

* Snapshot → rollback point for an existing VM.
* Golden Image/Template → source for creating new VMs.

The current server will remain the primary Base Server until the provisioning and cloning strategy is introduced.
