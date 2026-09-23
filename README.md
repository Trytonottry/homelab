# Homelab Infrastructure

Personal production-like infrastructure laboratory focused on **Linux, systems engineering, networking, virtualization, storage, observability, backup/DR and automation**.

The repository documents the current state of the lab, architectural decisions and planned infrastructure. It is intentionally kept closer to an infrastructure inventory/runbook than to a collection of random experiments.

## Goals

- Build and operate realistic Linux infrastructure.
- Practice production-oriented system administration and DevOps workflows.
- Self-host personal services without unnecessary cloud dependencies.
- Test networking, virtualization, storage, backup and disaster-recovery scenarios.
- Use the lab as a portfolio of practical infrastructure engineering work.

## Current architecture

### Compute

| Host | Platform | Role |
|---|---|---|
| **HOME / HP ProLiant DL380p Gen8** | Proxmox VE 9.2.x / Debian 13 | Main virtualization host |
| **HOME / Orange Pi Zero 3** | Linux | Auxiliary controller, monitoring/remote power workflows |
| **HOME / additional PCs and laptops** | Linux | Development, administration and test workloads |

The DL380p currently exposes **32 CPU threads and ~94 GiB RAM** to Proxmox. The host uses an HPE Smart Array P420i controller.

The DL380p is useful as a lab server, but its power consumption and noise are operational constraints. Hardware expansion is therefore treated as an engineering decision rather than a goal by itself.

### Network

Current home network is based on:

- **MikroTik hAP ac3**
- RouterOS 7.x
- LAN: `192.168.1.0/24`
- WireGuard management network: `10.255.255.0/30`
- Ethernet switching through unmanaged/SMB switches
- VLAN segmentation is planned where it provides a concrete security or operational benefit.

Remote access is designed around private management paths rather than exposing administration interfaces directly to the Internet.

### Virtualization

- **Proxmox VE**
- KVM virtual machines
- LXC containers
- Docker/Compose where containerization is appropriate
- k3s is used selectively for Kubernetes-oriented experiments rather than as the default deployment platform.

## Storage and backup

The storage architecture is being separated into two logical sites:

### HOME

Primary compute and active services.

### DACHA

Planned secondary storage/backup site with remote access and cold-storage characteristics.

The backup strategy currently includes:

- **Proxmox Backup Server (PBS)**
- **Kopia**
- Offline/cold-copy workflows
- Future storage hosts connected through SAS/HBA infrastructure

The lab follows the principle that **RAID is not a backup**. Important data must have independent copies and a tested recovery path.

## Observability

Current preference is **Zabbix** for infrastructure monitoring.

Monitoring priorities:

- host availability
- CPU/RAM/storage health
- network availability
- SMART and hardware health where available
- backup status
- service availability
- actionable alerts rather than dashboard-only telemetry

Grafana/Prometheus may be used for specific workloads, but they are not mandatory components of the platform.

## Services and tooling

Current/experimental infrastructure includes:

- **Komodo** for infrastructure/application management
- **Caddy / reverse proxy**
- **Docker / Compose**
- **Proxmox**
- **Zabbix**
- **Gotify**
- **Pi-hole / DNS tooling**
- **WireGuard / VPN**
- **Git / GitHub**
- **Python and Bash automation**

The stack is deliberately constrained. New components should solve a concrete problem instead of increasing platform complexity.

## Security principles

- Management interfaces are not exposed unnecessarily.
- SSH uses key-based authentication.
- Services run with least privilege where practical.
- Network segmentation is introduced when it materially reduces blast radius.
- Backups are separated from the primary failure domain.
- Credentials and secrets are never committed to the repository.
- Infrastructure changes should be reproducible and documented.

## Repository structure

- [HomeLab Overview](./HomeLab%20Overview.md) — entry point and documentation map
- [Homelab Infrastructure](./%F0%9F%8F%A0%20Homelab%20Infrastructure.md) — current infrastructure inventory
- [Network Topology](./%F0%9F%8C%90%20Homelab%20Network%20Topology%20Diagram.md) — logical network architecture
- [Infrastructure Engineering Project](./%F0%9F%A7%A0%20Homelab%20Infrastructure%20%E2%80%94%20DevOps%20%26%20System%20Engineering%20Project.md) — engineering goals and roadmap
- [Pictures](./Pictures%20HomeLab.md) — hardware photos

## Roadmap

### Near term

- Keep the current infrastructure documented and reproducible.
- Finish a clean network inventory.
- Improve Zabbix coverage and actionable alerting.
- Document backup/restore procedures.
- Reduce undocumented manual configuration.

### Medium term

- Introduce infrastructure-as-code where it removes repetitive work.
- Formalize HOME ↔ DACHA backup architecture.
- Improve network segmentation.
- Add tested disaster-recovery procedures.
- Build production-like deployment workflows for selected services.

### Long term

- Evolve the lab toward a small, resilient private platform.
- Use the infrastructure as a portfolio of real systems-engineering projects.
- Keep operational complexity proportional to actual requirements.

## Design rule

> **Prefer boring, observable, recoverable infrastructure over impressive but fragile architecture.**

## Author

**Trytonottry**

- GitHub: https://github.com/Trytonottry

---

_Last updated: September 2026_
