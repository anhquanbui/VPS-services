# Ubuntu Services Overview for VPS

This document provides a categorized overview of Ubuntu services commonly found on VPS servers. It also includes the command structure for managing these services.

---

## ✅ Essential Services (Keep Enabled)
These are required for the server to run properly:
- **systemd** (init system, cannot disable)
- **rsyslog** – system logging service
- **unattended-upgrades** – automatic security updates
- **NetworkManager** – manages network connections
- **containerd / docker** – required if using Docker

---

## ❌ Unnecessary Services (Safe to Disable on VPS)
These are often installed by default but not needed in most VPS environments:
- **ModemManager** – only needed for USB/3G/4G modems
- **multipathd** – used for SAN storage multipath
- **open-iscsi** – used for iSCSI storage
- **lvm2-monitor** – only required if using LVM volumes
- **pmie, pmlogger, pmproxy** – Performance Co-Pilot monitoring agents
- **podman, podman-* services** – redundant if Docker is already used
- **gpu-manager** – only relevant for systems with GPUs
- **setvtrgb, console-setup** – manage TTY console colors and fonts, not required on headless servers
- **pollinate** – fetches entropy from Ubuntu servers, safe to disable
- **blk-availability** – related to multipath/LVM, not needed
- **apport, apport-autoreport** – crash reporting, safe to disable

---

## ⚙️ Optional Services (Keep if Needed)
- **snapd & snap services** – only if you use Snap packages (otherwise safe to disable/remove)
- **cockpit** – web-based server manager, optional
- **certbot** – keep if using SSL certificates from Let’s Encrypt
- **qemu-guest-agent** – useful if running inside a virtualization platform (Proxmox, KVM, etc.)

---

## 🔧 Command Structure

### Check service status
```bash
systemctl status <service>
```

### Stop a service immediately
```bash
sudo systemctl stop <service>
```

### Disable a service (prevent starting at boot)
```bash
sudo systemctl disable <service>
```

### Mask a service (prevent manual or automatic activation)
```bash
sudo systemctl mask <service>
```

### Re-enable a service
```bash
sudo systemctl enable <service>
```

### Unmask a service
```bash
sudo systemctl unmask <service>
```

---

## 💡 Notes
- Masking a service provides stronger protection than disabling, as it prevents any process from starting it.  
- You can still run a masked service manually by calling its binary directly, but `systemd` won’t be able to start it.  
- Always verify with `systemctl status <service>` after changes.

