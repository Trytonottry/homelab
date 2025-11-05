

```text
                         ┌──────────────────────────┐
                         │     Acer Aspire A515-55  │
                         │   (Garuda Linux, Laptop) │
                         │   ────▶ ZeroTier Access  │
                         └──────────────┬───────────┘
                                        │
                                        ▼
                          ╔════════════════════════╗
                          ║   ZeroTier Virtual LAN  ║
                          ╚════════════════════════╝
                                        │
            ┌────────────────────────────────────────────────────┐
            │                    Local Network (LAN)              │
            │                     Ethernet 1 Gbit                │
            └────────────────────────────────────────────────────┘
                                        │
     ┌──────────────────────┬────────────────────────┬──────────────────────────┬────────────────────┐
     ▼                      ▼                        ▼                          ▼                    ▼
┌─────────────┐     ┌────────────────┐      ┌────────────────────┐     ┌──────────────────┐   ┌────────────────┐
│ Xiaomi TM1703│     │ HP DL380p Gen8│      │ Orange Pi 3 Zero  │     │ Mango Pi (IoT)   │   │ Mini PC WoWe   │
│ Debian       │     │ Proxmox VE    │      │ Armbian           │     │ Armbian          │   │ Lubuntu        │
│ ─ Gateway    │     │ ─ VM Host     │      │ ─ Wake-on-LAN     │     │ ─ MQTT / DNS     │   │ ─ Web Services │
│ ─ Monitoring │     │ ─ LXC / KVM   │      │ ─ Power Control   │     │ ─ Pi-hole        │   │ ─ Backups      │
└─────────────┘     └────────────────┘      └────────────────────┘     └──────────────────┘   └────────────────┘
        │                                                                               │
        │                                                                               │
        │                                                                               ▼
        │                                                                      ┌───────────────────┐
        │                                                                      │ Acer Veriton Z2650│
        │                                                                      │ Linux Mint        │
        │                                                                      │ ─ CI/CD Node      │
        │                                                                      └───────────────────┘
        │
        ▼
┌──────────────────────┐
│ Asus ET2701I-W8      │
│ Linux Mint           │
│ ─ GPU / Game Center  │
└──────────────────────┘

Legend:
- ───▶  Remote Access (ZeroTier)
- ─────  Ethernet Cable Connection
- Devices are linked via 1 Gbit LAN
- Xiaomi TM1703 acts as the central hub (gateway, monitor, and VPN entry)
  ```
  
