# Zero Trust Launcher

A self-hostable toolkit for securely launching and accessing Linux-based thin clients through a Cloudflare Zero Trust tunnel. Designed for homelab, enterprise-lite, or mobile workspace deployments.

---

## What It Does

Zero Trust Launcher is a modular system that:

- Creates a secure Cloudflare tunnel to a remote Linux session (RDP, NoMachine, or VNC)
- Auto-launches a remote desktop from any thin client (e.g. Raspberry Pi, laptop, virtual machine)
- Integrates 2FA, device posture checks, and access policies using Cloudflare Zero Trust
- Supports stealth mode (hiding services from public IP exposure)
- Enables fast redeployment via script or Docker

---

## Why I Built This

After deploying my own secure remote access solution using Cloudflare Tunnel and Linux, I realized how unintuitive most guides were for real-world use. This toolkit streamlines the entire process into a single, user-friendly stack—making secure remote desktops as easy to launch as SSH.

Built as part of **Project VELA**, this tool represents real-world engineering driven by need, not theory. It solves a personal pain point and offers a hardened, simplified platform for others to build on.

---

## Features

- Zero Trust cloud access without port forwarding
- Optional Docker deployment
- Systemd-based auto-launch at boot
- Launchable via GUI or command line
- Compatible with NoMachine, RDP, or VNC
- Network hardening (firewall, fail2ban, DNS leak check)

---

## Roadmap (see `/docs/roadmap.md`)

- [ ] Easy deploy script for Debian-based clients
- [ ] GUI launcher for selecting remote profile
- [ ] Built-in health monitor + logging
- [ ] Custom domain config flow
- [ ] SSH + desktop fallback mode

---

## Tech Stack

- Linux (Debian or Ubuntu preferred)
- Cloudflare Tunnel
- Bash, Python, or Ansible
- Remote desktop stack: NoMachine / xRDP / VNC

---

## Security Goals

- Prevent direct public exposure of any service
- Provide full session encryption and credential lockdown
- Hide infrastructure from scanners (Zero Trust gateway + WARP posture)

---

### Architecture Overview

```text
+----------------+       +----------------------+       +---------------------+
|  Thin Client   | <---> | Cloudflare Tunnel    | <---> |  Remote Linux Host  |
|  (Raspberry Pi)|       | (Zero Trust Gateway) |       |  (NoMachine / RDP)  |
+----------------+       +----------------------+       +---------------------+
                                |           |
                         2FA / Device Posture
```

---

This simple flow shows that the client never connects directly to the remote host’s IP—it only passes through Cloudflare’s encrypted tunnel and trust layer.

---

### Why Not Tailscale?

> Tailscale is incredible. But it solves a **different** problem.

| Feature | Tailscale | Zero Trust Launcher |
|--------|-----------|---------------------|
| VPN Mesh | ✅ Peer-to-peer | ❌ (Not needed) |
| Encrypted Tunnel | ✅ | ✅ |
| 2FA + Device Trust | 🔸 Limited via ACLs | ✅ Native (Cloudflare) |
| Port Exposure | ❌ NAT traversal | ✅ Fully hidden, cloud-pushed |
| Public access via domain | ❌ Requires hacks | ✅ Built-in |
| Designed for? | Teams on internal mesh | Gateway-style secure desktop |

**Conclusion:**  
Tailscale shines for trusted-device networks.  
**Zero Trust Launcher** is for **securely exposing a remote desktop** through a **cloud gateway**, without ever exposing ports or relying on device reputation alone.

---

Let me know if you’d like me to drop that into the `.md` file for you, or if you'd prefer it as part of the upcoming folder structure `.zip`.

Say **“Go for task breakdown”** when you’re ready to map the Zero Trust Launcher dev schedule.


## License

MIT License
