# 🦞 Installing OpenClaw on Low-End PCs

> A guide to running OpenClaw on older hardware by prioritizing lightweight environments and offloading heavy AI processing to the cloud.

---

## 🏗️ 1. Optimal Environment Choice

Older hardware often struggles with modern Windows overhead. A lightweight Linux distribution is highly recommended to keep the system responsive.

### Recommended OS

- **Ubuntu 22.04 LTS (Server/Lite)**: Stable and well-documented.
- **Debian 12 (Bookworm)**: Minimalist and extremely lean on RAM.
- **Raspberry Pi OS Lite (64-bit)**: Best for very low-power ARM-based hardware.

### Hardware Requirements

| Component   | Minimum for "Lite" Setup                                       |
| :---------- | :------------------------------------------------------------- |
| **RAM**     | 1 GB (Minimum)                                                 |
| **Storage** | SSD recommended (Avoid SD cards/HDDs for database performance) |
| **Node.js** | Version 22+ (Strictly required)                                |

---

## 🚀 2. Step-by-Step Installation

### A. Update & Install Node.js 22

OpenClaw requires a modern Node environment. Older versions will cause the gateway to crash.

```bash
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
sudo apt-get install -y nodejs
```

### B. Install OpenClaw

Use the official global installer:

```bash
sudo npm install -g openclaw@latest
```

### C. Run the Onboarding Wizard

```bash
openclaw onboard --install-daemon
```

> [!IMPORTANT]
> **Cloud vs. Local Models**: During onboarding, do **not** select local models (like Ollama). Choose a cloud provider (OpenAI, Anthropic, or Google Gemini) to keep CPU/RAM usage low.

---

## ⚙️ 3. Performance Optimizations

### Configure a Swap File

If you have 2 GB of RAM or less, a swap file is mandatory to handle execution spikes.

```bash
sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
```

### Use Headless Mode

Avoid running a Desktop Environment (GUI). Access the PC via **SSH** from another machine to save approximately 600 MB of RAM.

### Hardware Upgrades

If the PC uses an old mechanical hard drive, switching to a cheap **SATA SSD** is the single biggest performance gain for OpenClaw's logging and database operations.

### Limit Concurrency

In your configuration, ensure you are not running multiple agents simultaneously, as each agent maintains its own memory pool.

---

<p align="center">
  <i>Part of the <a href="../README.md">Docs & Guides Collection</a></i>
</p>
