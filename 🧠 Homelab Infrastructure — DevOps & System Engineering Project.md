
![Homelab Banner](https://img.shields.io/badge/Homelab-Linux%20Based-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge)
![Automation](https://img.shields.io/badge/Automation-Ansible%20%7C%20Proxmox%20%7C%20Docker-orange?style=for-the-badge)

## 🧩 Overview
This repository documents my **homelab infrastructure**, which serves as a personal **DevOps sandbox**, **virtualization cluster**, and **automation testbed**.  
The lab includes multiple physical and virtual machines connected through a gigabit Ethernet network and remotely accessible via **ZeroTier**.

> 🧠 *Goal: To maintain a fully automated, production-like environment for testing, CI/CD, and self-hosted services.*

---

## ⚙️ Hardware & System Layout

| Device | OS / Distro | Role | Connection |
|--------|--------------|------|-------------|
| **HP ProLiant DL380p Gen8** | Proxmox VE | Main virtualization host (VMs, LXC) | Ethernet |
| **Orange Pi 3 Zero** | Armbian | Wake-on-LAN controller | Ethernet |
| **Acer Veriton Z2650g** | Linux Mint | CI/CD & test node | Ethernet |
| **Asus ET2701I-W8** | Linux Mint | GPU / Game center | Ethernet |
| **Xiaomi TM1703** | Debian | Network monitoring, ZeroTier gateway | Ethernet |
| **Mango Pi** | Armbian | IoT / DNS / MQTT / Pi-hole | Ethernet |
| **Mini PC WoWe** | Lubuntu | Web services, backups | Ethernet |
| **Acer Aspire A515-55** | Garuda Linux | Development laptop, remote access | Wi-Fi + ZeroTier |

---

## 🧠 Core Services

| Service | Host | Description |
|----------|------|-------------|
| **Proxmox VE** | DL380p | VM and container management |
| **Grafana + Prometheus** | TM1703 | Centralized monitoring |
| **Pi-hole / AdGuard** | Mango Pi | DNS filtering and analytics |
| **FastAPI / Flask** | WoWe | API and backend services |
| **Jenkins / Git / CI/CD** | Veriton | Continuous integration and builds |
| **Home Assistant + MQTT** | Mango Pi | Smart automation layer |
| **ZeroTier / SSH** | All nodes | Remote management |

---

## 🧰 Tools & Stack

- **Virtualization:** Proxmox VE, LXC, KVM  
- **Automation:** Docker, Ansible (planned), Bash, Python  
- **Monitoring:** Prometheus, Grafana  
- **Networking:** ZeroTier, SSH, VLAN (planned)  
- **Security:** Fail2Ban, UFW, 2FA, SSH key-based auth  
- **Backup:** rsync, BorgBackup  

---

## 🔄 Automation

- Wake-on-LAN automation via **Orange Pi 3 Zero**  
- Backup sync between **Proxmox → WoWe**  
- Python/Bash management scripts for network and service control  
- Planned: Ansible playbooks for full configuration orchestration  

---

## 🧩 Key Projects Hosted

- 🤖 **Telegram Bot with CryptoBot payments** for GPT-based services  
- 🕵️ **Tender monitoring system** using Selenium + Telegram API  
- 🧠 **Local AI analysis of images and videos** via DL380p  
- 🔈 **Voice assistant system** (ASR + TTS processing)  
- 🌐 **Self-hosted FastAPI/Flask apps** with reverse proxy (Nginx)  

---

## 📈 Goals

✅ **Current:**  
- Functional virtualization cluster (Proxmox + Docker)  
- Full remote management via ZeroTier  
- Distributed nodes for CI/CD, IoT, and automation  

🚀 **Next steps:**  
- Deploy Ansible for infrastructure-as-code  
- Implement centralized logging (Loki)  
- Develop complete CI/CD pipeline for Python projects  
- Add Grafana dashboards for all system metrics  

---

## 🗺️ Architecture Diagram (Mermaid)

```mermaid
graph TD
    subgraph Remote Access
        A515[Acer Aspire A515-55<br>Garuda Linux<br>Dev Laptop]
    end

    subgraph ZeroTier Network
        A515 --> ZT[(ZeroTier)]
        ZT --> TM1703[Xiaomi TM1703<br>Debian<br>Gateway + Monitoring]
    end

    subgraph Local Network (1 Gbit Ethernet)
        TM1703 --> DL380p[HP ProLiant DL380p Gen8<br>Proxmox VE<br>Main Host]
        TM1703 --> OPI[Orange Pi 3 Zero<br>Armbian<br>Wake-on-LAN]
        TM1703 --> WoWe[Mini PC WoWe<br>Lubuntu<br>Web / Backup]
        TM1703 --> Veriton[Acer Veriton Z2650g<br>Linux Mint<br>CI/CD Node]
        TM1703 --> Mango[Mango Pi<br>Armbian<br>IoT / DNS / MQTT]
        TM1703 --> Asus[Asus ET2701I-W8<br>Linux Mint<br>GPU / Game Center]
    end

    classDef device fill:#1f2937,stroke:#4b5563,color:#fff,stroke-width:1px;
    class DL380p,OPI,WoWe,Veriton,Mango,Asus,TM1703,A515 device;
```

> 🧩 _The diagram can be edited directly in Markdown to add new nodes, VLANs, or virtual machines._

---

## 🧑‍💻 Author

**[Твоё имя / GitHub Nickname]**

- 💬 Telegram: [@твой_ник]
    
- 💻 GitHub: [github.com/твой_ник]
    
- ✉️ Email: [твоя_почта@example.com]
    

> 🧠 “Homelab is not just a hobby — it’s a personal cloud, a DevOps lab, and a place where ideas become infrastructure.”