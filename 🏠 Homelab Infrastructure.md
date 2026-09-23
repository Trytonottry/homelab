# 🏠 Homelab Infrastructure

## 1. Purpose

This document describes the current physical infrastructure of the HOME homelab.

The lab is used for:

- Linux/system administration practice
- virtualization
- self-hosted services
- networking experiments
- storage and backup
- observability
- automation
- production-like failure and recovery testing

Planned infrastructure is explicitly marked as **planned** and is not treated as deployed inventory.

---

## 2. Compute

### HP ProLiant DL380p Gen8

**Role:** primary virtualization host.

| Property | Current state |
|---|---|
| Hypervisor | Proxmox VE 9.2.x |
| Base OS | Debian 13 (trixie) |
| CPU | 2 × Xeon E5-2650L |
| CPU threads | 32 |
| RAM | ~94 GiB visible to Proxmox |
| RAID controller | HPE Smart Array P420i |
| Workloads | KVM VMs, LXC, infrastructure services |

The server is intentionally treated as a lab platform rather than as a production-critical single point of failure.

Power consumption and acoustics are significant constraints.

### Orange Pi Zero 3

**Role:** auxiliary management/controller node.

Potential workloads include:

- Wake-on-LAN
- hardware/environment telemetry
- emergency management workflows
- lightweight network utilities

Small ARM nodes are useful for management-plane functions because they can remain available while the main compute host is powered down.

---

## 3. Network

### Router

**MikroTik hAP ac3**

- RouterOS 7.x
- LAN: `192.168.1.0/24`
- WireGuard management network: `10.255.255.0/30`

The MikroTik is the primary home network gateway.

### Switching

The current environment contains multiple Ethernet switches, including unmanaged switches.

The network is intentionally kept simple until segmentation provides a measurable operational or security benefit.

### Planned network improvements

- formal network inventory
- VLAN segmentation
- documented management plane
- clearer separation of trusted, server and IoT traffic
- monitoring of critical network devices

---

## 4. Virtualization

The main virtualization layer is **Proxmox VE**.

Workload types:

- KVM virtual machines
- LXC containers
- Docker/Compose inside appropriate VMs
- selective k3s experiments

The default principle is to avoid nesting technologies without a concrete reason. For example, Kubernetes is not used merely because the lab can run it.

---

## 5. Storage

Current storage work is split between active HOME infrastructure and a planned remote/secondary site.

### HOME

Active compute and service storage.

### DACHA — planned

The future DACHA site is intended to provide:

- secondary backup storage
- cold-copy storage
- remote recovery capability
- an independent failure domain

Planned storage infrastructure includes SAS-connected disks and dedicated storage hosts.

Hardware that has only been considered or planned is **not** listed as current inventory.

---

## 6. Backup and recovery

Backup tooling currently includes:

- **Proxmox Backup Server**
- **Kopia**
- cold/offline copies

Current logical backup data is approximately:

- PBS: ~7.6 TiB
- Kopia: ~5.1 TiB

The target architecture is based on multiple independent copies rather than relying on RAID alone.

Important recovery procedures should eventually be documented as executable runbooks:

1. identify failure
2. restore infrastructure
3. restore application data
4. verify integrity
5. return service to operation

A backup that has never been restored is not considered operationally verified.

---

## 7. Observability

Primary infrastructure monitoring direction:

**Zabbix**

Monitoring should cover:

- availability
- resource utilization
- disk capacity
- disk health
- hardware health
- network health
- backup jobs
- critical services

**Gotify** is used for actionable notifications.

Grafana/Prometheus remain optional tools for workloads where their model provides additional value.

---

## 8. Service management

Current infrastructure tooling includes:

- Komodo
- Docker / Compose
- Caddy
- Git / GitHub
- Bash
- Python
- WireGuard
- Zabbix
- Gotify

The lab does not aim to run every popular DevOps tool.

The preferred architecture is the smallest stack that provides:

**automation → observability → backup → recovery**

---

## 9. Security model

Core principles:

- no unnecessary public exposure
- private management paths
- SSH key authentication
- least privilege
- network segmentation where justified
- isolated backup copies
- secrets outside Git
- regular patching
- documented recovery procedures

The lab is also used to test security boundaries and failure scenarios safely.

---

## 10. Current engineering priorities

1. Documentation and inventory accuracy
2. Monitoring and alerting
3. Backup verification
4. Network structure
5. Automation of repetitive operations
6. HOME ↔ DACHA resilience
7. Only then: additional platform components

---

## 11. Engineering principle

> **If a component increases operational complexity without improving reliability, security, observability or learning value, it probably does not belong in the lab.**

_Last updated: September 2026_
