# Ubuntu Services Optimization Guide

This document summarizes common `systemd` services on Ubuntu, categorized by whether they are required or optional for a VPS setup (SSDNodes).  
Goal: minimize unnecessary resource usage while keeping essential components for running **Docker, Cockpit, VSCode, Jupyter, Portainer, Cloudflare Tunnel**.

---

## 🔧 Essential Services
These should stay enabled for a stable system:

- **systemd-logind** – Manages login sessions.
- **rsyslog** – System logging service.
- **NetworkManager** – Basic network management.
- **systemd-resolved** – DNS resolver.
- **unattended-upgrades** – Automatic security updates (recommended).
- **docker / containerd** – Container runtime (Docker backend).
- **cockpit** – Web-based server management (if you use it).
- **cloudflared** (or tunnel service) – Reverse proxy via Cloudflare.

---

## 🚫 Unnecessary Services (Safe to Disable/Mask)
These are not required for most VPS setups and can be disabled to save resources:

- **setvtrgb** – Console color setup.
- **qemu-guest-agent** – Only needed if KVM host requires guest management.
- **pollinate** – Seeds random number generator (mainly for cloud-init).
- **podman*** – Alternative container runtime (disable if using Docker).
- **pmproxy / pmlogger / pmie** – Performance Co-Pilot tools (rarely used).
- **open-iscsi** – iSCSI client, not needed unless you use remote block storage.
- **multipathd** – Multipath device management (SAN storage only).
- **netplan-ovs-cleanup** – Open vSwitch cleanup (not needed unless using OVS).
- **networkd-dispatcher** – Events for systemd-networkd (you use NetworkManager).
- **NetworkManager-wait-online** – Waits for network on boot (slows boot).
- **ModemManager** – For 3G/4G modems (not needed on VPS).
- **lvm2-monitor** – Logical Volume Manager monitoring (not needed, no LVM).
- **gpu-manager** – NVIDIA GPU management (not needed on headless VPS).
- **apport / apport-autoreport** – Ubuntu crash reporting (safe to disable).
- **console-setup** – Console keymap/font setup (safe to disable).
- **blk-availability** – Multipath device check (not needed on VPS).

---

## 🟡 Optional Services (Enable if Needed)
These depend on your specific use case:

- **snapd** – Snap package manager (only enable if you use snap packages).
- **certbot** – For SSL certificate management (keep if you use Let's Encrypt).
- **firewalld / ufw** – Firewall (useful if you need host-level firewalling).

---

## ✅ Recommendations
- Keep the **essential services** enabled at all times.
- Disable/mask the **unnecessary services** to reduce resource usage and boot time.
- Enable **optional services** only if your workflow requires them.
- For web apps (Jupyter, VSCode, Portainer, Cockpit), manage SSL via **Certbot + Nginx/Cloudflare Tunnel**.

---
