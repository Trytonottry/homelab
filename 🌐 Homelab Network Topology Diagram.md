# 🌐 Homelab Network Topology

## Logical topology

```text
                         Internet
                            │
                            ▼
                    ┌────────────────┐
                    │ MikroTik hAP   │
                    │ ac3 / RouterOS │
                    └───────┬────────┘
                            │
                 LAN 192.168.1.0/24
                            │
              ┌─────────────┴─────────────┐
              │                           │
              ▼                           ▼
      ┌───────────────┐          ┌──────────────────┐
      │ Ethernet      │          │ Management / VPN │
      │ switches      │          │ WireGuard        │
      └───────┬───────┘          │ 10.255.255.0/30 │
              │                   └──────────────────┘
       ┌──────┼───────────┬───────────────┐
       │      │           │               │
       ▼      ▼           ▼               ▼
    Proxmox  Orange Pi   Linux clients   Other LAN
    DL380p   Zero 3      / test nodes    devices
       │
       ├── KVM VMs
       ├── LXC containers
       └── Docker workloads

                 Backup / secondary site
                         │
                         ▼
                ┌──────────────────┐
                │ DACHA (planned)  │
                │ Storage + backup  │
                └──────────────────┘
```

## Addressing

| Network | Purpose |
|---|---|
| `192.168.1.0/24` | HOME LAN |
| `10.255.255.0/30` | WireGuard management network |

The exact per-host addressing should be maintained in a separate inventory as the environment grows.

## Network principles

### 1. Management plane

Administrative access should use dedicated/private paths wherever possible.

### 2. Segmentation

VLANs are planned, but only where they provide a concrete security or operational benefit.

Potential future zones:

- management
- servers
- clients
- IoT
- guest
- storage/backup

### 3. Remote access

Remote administration should not depend on exposing Proxmox, storage management or other administrative interfaces directly to the public Internet.

### 4. Resilience

The network design must account for:

- router failure
- Internet outage
- loss of the main compute host
- loss of HOME
- inability to reach one physical site

The future DACHA site is intended to provide a separate recovery domain rather than simply another LAN segment.

## Current vs planned

**Current**

- MikroTik hAP ac3
- RouterOS 7.x
- `192.168.1.0/24`
- WireGuard management network
- Ethernet switching
- Proxmox host
- auxiliary ARM node

**Planned**

- VLAN segmentation
- more explicit management/storage networks
- independent secondary-site connectivity
- improved network monitoring

_Last updated: September 2026_
