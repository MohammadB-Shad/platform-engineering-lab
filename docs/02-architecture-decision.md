# Architecture Decisions

## Architecture Approach

The lab will be built incrementally using a production-oriented approach.

The initial architecture will remain simple and understandable. Additional complexity will be introduced only when business or technical requirements justify it.

The guiding principle is:

> Start simple, understand the system deeply, and scale the architecture as the business grows.

## Initial Architecture

The initial infrastructure will be based on virtual machines running on VMware Workstation.

Network segmentation will be implemented from the beginning:

* Management Network
* Application Network

Servers will initially be deployed as individual virtual machines.

## Kubernetes Decision

Kubernetes will not be introduced at the beginning of the project.

The initial application environment is not large enough to justify Kubernetes complexity.

The project will first establish:

* Linux administration
* Networking
* Git
* Docker
* CI/CD
* Monitoring
* Logging
* Security
* Automation

Kubernetes will be introduced later when the application architecture and operational requirements justify container orchestration.

## Server Role Strategy

Servers will start from a clean Base Server configuration.

The Base Server will contain:

* Operating system baseline
* Network configuration
* Storage configuration
* SSH
* Common administration tools
* Time synchronization
* Basic security controls
* Firewall

Role-specific software will be installed only after the server role is defined.

Examples:

* Git server
* CI/CD server
* Monitoring server
* Application server
* Database server

This keeps the Base Server generic and reusable.

## Network Segmentation

Management and Application traffic will use separate logical networks.

### Management

Used for:

* SSH
* Server administration
* Monitoring
* Automation

### Application

Used for:

* Application communication
* Internal service communication

The Management network will not be used as the default Internet gateway.

## Scaling Strategy

The infrastructure will evolve gradually.

The expected progression is:

```text
Single Server
    ↓
Multiple Servers
    ↓
Service Separation
    ↓
Automation
    ↓
High Availability
    ↓
Container Orchestration
```

Each stage will be introduced when there is a practical reason to do so.

## Operational Philosophy

Every major infrastructure change should follow:

```text
Requirement
    ↓
Design
    ↓
Implementation
    ↓
Verification
    ↓
Documentation
    ↓
Operation
    ↓
Troubleshooting
    ↓
Automation
```

The objective is not only to build the environment, but also to understand how to operate and troubleshoot it.
