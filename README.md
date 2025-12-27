🛡️ Home Privacy & Media Hub
A Dockerized Ad-Blocking & Secure Remote Access Stack
This project documents the deployment of a privacy-focused home server running on a Raspberry Pi 4. The goal was to centralize network-level ad-blocking, establish a secure "phone home" VPN tunnel, and provide network-attached storage (NAS) for media streaming.

🚀 Hardware
Vilros Raspberry Pi 4 Model B Kit (8GB)

1TB Aiolo External HDD

Amazon Fire TV Stick

Cat 5e Ethernet cable

🚀 The Tech Stack
Host OS: Raspberry Pi OS (Legacy, 64-bit) Lite

Management UI: OpenMediaVault (OMV 7.0)

Container Engine: Docker & Docker Compose

Network Security: Pi-hole (DNS Sinkhole)

Remote Access: WireGuard (via wg-easy)

Storage Protocol: SMB/CIFS for local NAS, DNS (53), WireGuard (UDP 51820), HTTP (8096).


🏗️ Architecture Overview
The system is designed with Isolation and Persistence as core principles. Using Docker Compose, each service runs in a dedicated containerized environment with a custom internal bridge network.

1. Pi-hole (The Guard)
Function: Network-wide ad and tracker blocking.

Key Configuration: Integrated with a custom local subnet (10.2.0.0/24) to allow seamless communication with the VPN gateway.

Impact: Reduced telemetry and bandwidth usage across all home devices (Smart TVs, Mobile, IoT).

2. WireGuard (The Tunnel)
Function: Secure, encrypted remote access to the home network.

Use Case: Accessing the local NAS and Jellyfin media server while traveling without exposing ports directly to the public internet.

🛠️ Lessons Learned & Technical Challenges
Troubleshooting the "Recursive DNS Loop"

One of the primary challenges involved the "Chatty Router" effect. After permitting the router to query the Pi-hole, the block rate appeared to drop to ~4%. Through log analysis, I identified that this wasn't a failure of the ad-blocker, but a statistical dilution caused by the high frequency of non-ad connectivity checks from the router.

Dockerized Infrastructure
I moved from manual installations to Infrastructure as Code (IaC). By defining the stack in a compose.yaml file, the entire server can be rebuilt or migrated in minutes.

📂 Project Structure
 home-server
├── compose.yaml         # The "Blueprint" for the entire stack
├── pihole-config        # Persistent data for DNS settings
├── wireguard-config     # VPN client profiles and keys
└── shared-storage       # NAS mount point for media

📈 Future Roadmap
 - Unbound Integration: Moving from upstream DNS providers to a local recursive resolver for maximum privacy.

 - Automated Backups: Implementing an rsync schedule to mirror the primary drive to a secondary disk (Strategy: Backup > RAID 1 for   Pi-based USB storage).

 - Media Streaming: Finalizing the Jellyfin deployment for hardware-accelerated transcoding.