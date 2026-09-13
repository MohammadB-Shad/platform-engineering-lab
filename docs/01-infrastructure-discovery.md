# Infrastructure Discovery

## Business Information

The business scenario has not been fully defined yet.

The lab will initially focus on building a production-like infrastructure foundation and will gradually introduce application, operational and business requirements.

## Application Information

The application architecture has not been defined yet.

The initial infrastructure will be built in a way that allows application workloads to be introduced later without requiring a redesign of the basic network and server foundation.

## Users and Growth

User volume and growth requirements have not been defined yet.

The infrastructure will initially prioritize simplicity and operational clarity. Scaling will be introduced when the simulated business requirements justify it.

## Availability Requirements

High Availability requirements have not been defined yet.

The initial environment will start with a simple architecture and will evolve toward redundancy when the application and business requirements require it.

## Security Requirements

Initial security requirements include:

* Network segmentation
* Dedicated Management network
* Restricted SSH access
* Root SSH password login disabled
* Firewall enabled
* Security updates enabled
* Time synchronization enabled

More advanced security controls will be introduced progressively as the environment grows.

## Backup and Disaster Recovery

Backup and Disaster Recovery requirements have not yet been finalized.

The lab will later introduce:

* Backup strategy
* Restore testing
* Disaster Recovery scenarios
* Failover exercises

## Monitoring Requirements

Monitoring requirements will be defined as services are introduced.

The monitoring strategy will eventually cover:

* Infrastructure health
* Resource utilization
* Service availability
* Application health
* Logs
* Alerts

## Budget and Constraints

The lab is built using local virtualization infrastructure.

Current constraints:

* VMware Workstation is used as the virtualization platform.
* The host provides 64 GB RAM.
* Existing Ubuntu Server 22.04.4 LTS installation media is used.
* The environment is designed for learning and experimentation rather than production deployment.

The infrastructure should remain simple enough to troubleshoot and understand while providing a realistic foundation for future expansion.
