Raspberry Pi Privacy Hub & Media Server

Project Overview
This project demonstrates the design and deployment of a containerized home lab server running on a Raspberry Pi 4. The primary goal was to reclaim network privacy and establish secure remote access. The system centralizes network-wide ad-blocking (DNS sinkhole), provides a secure VPN tunnel for accessing home resources from abroad, and hosts a local media server for streaming to client devices like Amazon Fire Sticks.

Technologies Used
Hardware: Vilros Raspberry Pi 4 Model B Kit (8GB), 1TB Aiolo External HDD, Amazon Fire TV Stick, Cat 5e Ethernet cable.

Software: Raspberry Pi OS (Legacy, 64-bit) Lite, OpenMediaVault (OMV 7.0), Docker, Docker Compose.

Services: Pi-hole (DNS Ad-Blocker), WireGuard (VPN via wg-easy), Jellyfin (Media Server).

Protocols: SMB/CIFS (File Sharing), DNS (53), WireGuard (UDP 51820), HTTP (8096).

Key Features
Network-Wide Ad Blocking: Configured Pi-hole as the primary local DNS server, reducing tracking telemetry and advertisements across all LAN devices (Smart TVs, Phones, PC).

Secure Remote Access: Deployed a WireGuard VPN tunnel to allow secure "phone home" capabilities, enabling access to the NAS, Media Server, and DNS Ad-Blocker from public Wi-Fi networks.

Containerized Architecture: Utilized docker-compose to define the entire infrastructure as code, using a custom internal bridge network (10.2.0.0/24) with static IP assignments for service stability.

Hardware Acceleration: Enabled /dev/dri mapping in Docker to utilize the Raspberry Pi 4's GPU for efficient media transcoding in Jellyfin.

DNS Strategy: Implemented a strict DNS configuration (Secondary DNS set to 0.0.0.0) to force all client traffic through the sinkhole, preventing router-level bypass.

Configuration Details
Infrastructure: See compose.yaml for the complete service definition, port mappings, and volume persistence strategy.

Networking: Custom Docker subnet configured at 10.2.0.0/24 to isolate container traffic from the main LAN (192.168.1.0/24).

Storage: Data persistence handled via bind mounts to the external USB HDD managed by OpenMediaVault (absolute path mapping).